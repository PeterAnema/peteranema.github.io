---
layout: post
title: "Peter Anema's Github Pages Site & Blog"
date: 2021-02-01
---

Well. Finally got around to putting this website together and started blogging. 

List of my repositories as of 2021-02-02:

* [dash-sample-apps](https://github.com/PeterAnema/dash-sample-apps)
* [novi-data-science](https://github.com/PeterAnema/novi-data-science)
* [peteranema.github.io](https://github.com/PeterAnema/peteranema.github.io)
* [python-data-science](https://github.com/PeterAnema/python-data-science)
* [python-programming-sandbox](https://github.com/PeterAnema/python-programming-sandbox)
* [springboot-01-hello-world](https://github.com/PeterAnema/springboot-01-hello-world)
* [springboot-02-restful-controller](https://github.com/PeterAnema/springboot-02-restful-controller)
* [springboot-03-crud-controller](https://github.com/PeterAnema/springboot-03-crud-controller)
* [springboot-04-spring-data-jdbc](https://github.com/PeterAnema/springboot-04-spring-data-jdbc)
* [springboot-05-spring-data-jpa-customers](https://github.com/PeterAnema/springboot-05-spring-data-jpa-customers)
* [springboot-06-demo-spring-jpa-clients](https://github.com/PeterAnema/springboot-06-demo-spring-jpa-clients)
* [springboot-09-spring-security](https://github.com/PeterAnema/springboot-09-spring-security)
* [springboot-10-spring-security](https://github.com/PeterAnema/springboot-10-spring-security)
* [springboot-11-security-with-custom-users-table](https://github.com/PeterAnema/springboot-11-security-with-custom-users-table)
* [springboot-12-security-with-users-table](https://github.com/PeterAnema/springboot-12-security-with-users-table)
* [springboot-13-security-with-user-entity](https://github.com/PeterAnema/springboot-13-security-with-user-entity)
* [springboot-14-security-with-user-service](https://github.com/PeterAnema/springboot-14-security-with-user-service)
* [springboot-15-security-with-jwt](https://github.com/PeterAnema/springboot-15-security-with-jwt)
* [springboot-20-spring-https](https://github.com/PeterAnema/springboot-20-spring-https)
* [springboot-25-file-upload-basic](https://github.com/PeterAnema/springboot-25-file-upload-basic)
* [springboot-26-file-upload](https://github.com/PeterAnema/springboot-26-file-upload)
* [springboot-30-spring-boot-starter-test-assertj](https://github.com/PeterAnema/springboot-30-spring-boot-starter-test-assertj)
* [springboot-31-spring-boot-starter-test-junit-jupiter](https://github.com/PeterAnema/springboot-31-spring-boot-starter-test-junit-jupiter)
* [springboot-40-many-to-many](https://github.com/PeterAnema/springboot-40-many-to-many)
* [springboot-42-many-to-many](https://github.com/PeterAnema/springboot-42-many-to-many)
* [springboot-43-many-to-many-with-fields](https://github.com/PeterAnema/springboot-43-many-to-many-with-fields)
* [springboot-50-student-course](https://github.com/PeterAnema/springboot-50-student-course)
* [springboot-51-books-api](https://github.com/PeterAnema/springboot-51-books-api)

This list was generated from the GitHub API [GitHub REST API](https://docs.github.com/en/rest) with this Python script:

{% highlight python linenos %}
import requests

github_username = 'PeterAnema'

url = f'https://api.github.com/users/{github_username}/repos'

r = requests.get(url)

if r.status_code == 200:

    for repo in sorted(r.json(), key = lambda repo: repo['name']):
        print(f'* [{repo["name"]}]({repo["html_url"]})')
{% endhighlight %}
