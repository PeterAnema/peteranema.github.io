# Mappings and Associations in Springboot

## Mapping

### Class level
| annotation | attributes | description |
| --- | --- | --- |
| @Entity | name | |
| @Embeddable | | |

### Attribute level
| annotation | attributes | description |
| --- | --- | --- |
| @Basic | | the simplest type of mapping to a database column |
| @Column | name,length, nullable, precision, scale, unique | specifies the mapped column |
| @Id | use a wrapper type (e.g. Long or Integer) | specifies the entity identifier<br>An entity must always have an identifier attribute |
| @GeneratedValue | strategy = GenerationType.AUTO<br>AUTO, IDENTITY, SEQUENCE or TABLE |  |
| @EmbeddedId |  | a composite identifier |
| @IdClass | | is used if the current entity defined a composite identifier. The IdClass simply acts as a "shadow" |
| @NaturalId | | |
| @MapsId | | derived identifiers which allow an entity to borrow the identifier from a many-to-one or one-to-one association |
| @PrimaryKeyJoinColumn | | |
| @Enumerated | | to specify that an entity attribute represents an enumerated type |
| @Generated| NEVER, INSERT, ALWAYS | Generated properties are properties that have their values generated by the database |
| @CreationTimestamp |  |  |
| @UpdateTimestamp |  |  |

## Associations

| annotation | attributes |  description |
| --- | --- | --- |
| @OneToOne |   |   |
| @OneToMany |   |   |
| @ManyToOne |   |   |
| @ManyToMany |   |   |
| @JoinColumn | to specify the FOREIGN KEY column |   |
| @JoinTable | to specify the link table between two other database tables |   |
| @MapKey | the key of a java.util.Map association |   |
| @MapsId | annotation is used to specify that the entity identifier is mapped by the currently annotated @ManyToOne or @OneToOne association |   |
| @ForeignKey | to specify the associated foreign key of a @JoinColumn mapping.<br>The @ForeignKey annotation is only used if the automated schema generation tool is enabled, in which case, it allows you to customize the underlying foreign key definition.   |   |

### @ManyToOne

@ManyToOne is the most common association, having a direct equivalent in the relational database as well (e.g. foreign key), and so it establishes a relationship between a child entity and a parent.

```java
@ManyToOne
@JoinColumn(name = "person_id",
            foreignKey = @ForeignKey(name = "PERSON_ID_FK")
)
```

### @OneToMany

The @OneToMany association links a parent entity with one or more child entities. If the @OneToMany doesn’t have a mirroring @ManyToOne association on the child side, the @OneToMany association is unidirectional. If there is a @ManyToOne association on the child side, the @OneToMany association is bidirectional and the application developer can navigate this relationship from both ends.

The @OneToMany association is by definition a parent association, regardless of whether it’s a unidirectional or a bidirectional one. Only the parent side of an association makes sense to cascade its entity state transitions to children.

When using a unidirectional @OneToMany association, Hibernate resorts to using a link table between the two joining entities.

```java
@OneToMany(cascade = CascadeType.ALL, 
           orphanRemoval = true)
private List<Phone> phones = new ArrayList<>();
```

The bidirectional @OneToMany association also requires a @ManyToOne association on the child side. Although the Domain Model exposes two sides to navigate this association, behind the scenes, the relational database has only one foreign key for this relationship.

Every bidirectional association must have one owning side only (the child side), the other one being referred to as the inverse (or the mappedBy) side.

Whenever a bidirectional association is formed, the application developer must make sure both sides are in-sync at all times.

Unlike the unidirectional @OneToMany, the bidirectional association is much more efficient when managing the collection persistence state. Every element removal only requires a single update (in which the foreign key column is set to NULL), and, if the child entity lifecycle is bound to its owning parent so that the child cannot exist without its parent, then we can annotate the association with the orphanRemoval attribute and dissociating the child will trigger a delete statement on the actual child table row as well.

##### Parent side

```java
@OneToMany(mappedBy = "person",
           cascade = CascadeType.ALL, 
           orphanRemoval = true)
private List<Phone> phones = new ArrayList<>();
```

##### Child side - Owner
```java
@ManyToOne
private Person person;
```

### @OneToOne

The @OneToOne association can either be unidirectional or bidirectional. A unidirectional association follows the relational database foreign key semantics, the client-side owning the relationship. A bidirectional association features a mappedBy @OneToOne parent side too.

From a relational database point of view, the underlying schema is identical to the unidirectional @ManyToOne association, as the client-side controls the relationship based on the foreign key column.

##### Unidirectional @OneToOne
```java
@OneToOne
@JoinColumn(name = "details_id")
private PhoneDetails details;
```

But then, it’s unusual to consider the Phone as a client-side and the PhoneDetails as the parent-side because the details cannot exist without an actual phone. A much more natural mapping would be the Phone were the parent-side, therefore pushing the foreign key into the PhoneDetails table. This mapping requires a bidirectional @OneToOne association as you can see in the following example:

#### Bidirectional @OneToOne

##### Parent side
```java
@OneToOne(
    mappedBy = "phone",
    cascade = CascadeType.ALL,
    orphanRemoval = true,
    fetch = FetchType.LAZY
)
private PhoneDetails details;
```

##### Child side
```java
@OneToOne(fetch = FetchType.LAZY)
@JoinColumn(name = "phone_id")
private Phone phone;
```
It is much more efficient to use unidirectional @OneToOne associations with the @MapsId annotation in place.

### @ManyToMany

The @ManyToMany association requires a link table that joins two entities. Like the @OneToMany association, @ManyToMany can be either unidirectional or bidirectional.

#### Unidirectional @ManyToMany

Just like with unidirectional @OneToMany associations, the link table is controlled by the owning side.

For @ManyToMany associations, the REMOVE entity state transition doesn’t make sense to be cascaded because it will propagate beyond the link table.

```java
@ManyToMany(cascade = {CascadeType.PERSIST, CascadeType.MERGE})
private List<Address> addresses = new ArrayList<>();
```

#### Bidirectional @ManyToMany

A bidirectional @ManyToMany association has an owning and a mappedBy side. 

To preserve synchronicity between both sides, it’s good practice to provide helper methods for adding or removing child entities.

```java
@ManyToMany(cascade = {CascadeType.PERSIST, 
                       CascadeType.MERGE})
private List<Address> addresses = new ArrayList<>();
```

```java
@ManyToMany(mappedBy = "addresses")
private List<Person> owners = new ArrayList<>();
```

#### Bidirectional many-to-many with link entity

##### Side 1
```java
@OneToMany(mappedBy = "person",
           cascade = CascadeType.ALL,
           orphanRemoval = true
)
private List<PersonAddress> addresses = new ArrayList<>();
```

#### Association class
```java
@Id
@ManyToOne
private Person person;

@Id
@ManyToOne
private Address address;
```

##### Side 2
```java
	@OneToMany(
		mappedBy = "address",
		cascade = CascadeType.ALL,
		orphanRemoval = true
	)
	private List<PersonAddress> owners = new ArrayList<>();
```

## Inheritance

Although relational database systems don’t provide support for inheritance, Hibernate provides several strategies to leverage this object-oriented trait onto domain model entities:

#### MappedSuperclass
Inheritance is implemented in the domain model only without reflecting it in the database schema. See MappedSuperclass.

#### Single table
The domain model class hierarchy is materialized into a single table which contains entities belonging to different class types. See Single table.

#### Joined table
The base class and all the subclasses have their own database tables and fetching a subclass entity requires a join with the parent table as well. See Joined table.

#### Table per class
Each subclass has its own table containing both the subclass and the base class properties. See Table per class.


## Links

* https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#associations-many-to-many
* https://hellokoding.com/many-to-many-relationship-mapping-in-jpa-and-hibernate/
* https://en.wikipedia.org/wiki/Data_modeling
* http://www.agiledata.org/essays/dataModeling101.html