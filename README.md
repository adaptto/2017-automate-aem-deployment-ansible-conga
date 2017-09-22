adaptTo() 2017 - Automate AEM Deployment with Ansible and wcm.io CONGA
======================================================================

Code samples for talk at adaptTo() 2017 in Berlin:<br/>
https://adapt.to/2017/en/schedule/automate-aem-deployment-with-ansible-and-wcm-io-conga.html

Requirements
------------

* Java 8
* Maven 3.3.9+
* AEM 6.3 Quickstart JAR & license.properties
* Ansible 2.2+
* AWS Account (and your credentials properly configured for [Boto](https://github.com/boto/boto3))

Try it out
----------

* Execute `ansible-galaxy install -r requirements.yml` to install the required Ansible roles from GitHub.
* Place the `AEM_6.3_Quickstart.jar` and  `license.properties` files into the `files`  directory.
* Create two `t2.medium` EC2 instances with an Ubuntu AMI and at least the following tags:

    Key|Value
    ---|---
    Environment|adaptTo_development
    Role|aem
    
    > Note that you need to [bootstrap Python on the instances](https://gist.github.com/gwillem/4ba393dceb55e5ae276a87300f6b8e6f) when using Ubuntu 16.04+, otherwise you'll get confusing "connection refused" messages from Ansible.

* Tag one instance as `aem-author`, the other as `aem-publish` with the `Node` tag.
* Execute `ansible-playbook setup.yml -e conga_environment=development` to install AEM 6.3 and deploy the [wcm.io Samples](https://github.com/wcm-io/wcm-io-samples) on the newly created instances.

