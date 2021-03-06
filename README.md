Ansible Role: Jenkins on OpenShift
[![Build Status](https://travis-ci.org/siamaksade/ansible-openshift-jenkins.svg?branch=master)](https://travis-ci.org/siamaksade/ansible-openshift-jenkins)
=========

Ansible Role for deploying Jenkins CI engine on OpenShift


Role Variables
------------

|Variable                    | Default Value     | Description   |
|----------------------------|-------------------|---------------|
|`disable_admin_monitors`    | false | Disable cpu-intensive update tasks on Jenkins bootstrap which pronolgs the start up time |
|`deploy_jenkins`            | true              | Deploy Jenkins |
|`jenkins_service_name`      | jenkins           | Jenkins service name on OpenShift  |
|`jenkins_max_mem`           | 2Gi               | Max memory allocated to Jenkins container |
|`jenkins_min_mem`           | 512Mi             | Min memory allocated to Jenkins container |
|`jenkins_max_cpu`           | 1                 | Max cpu allocated to Jenkins container |
|`jenkins_min_cpu`           | 200m              | Min cpu allocated to Jenkins container |
|`jenkins_image_tag`         | 2                 | Jenkins image tag to deploy. Specify tag for either [OpenShift Container Platform](https://access.redhat.com/containers/?tab=tags#/registry.access.redhat.com/openshift3/jenkins-2-rhel7) or [OpenShift Origin](https://hub.docker.com/r/openshift/jenkins-2-centos7/tags/)|
|`project_name`              | jenkins           | OpenShift project name for the Jenkins container  |
|`project_display_name`      | Jenkins           | OpenShift project display name for the Jenkins container  |
|`project_desc`              | Jenkins CI Engine | OpenShift project description for the Jenkins container |
|`project_annotations`       | -                 | OpenShift project annotations for the Jenkins container |
|`openshift_cli`             | oc                | OpenShift CLI command and arguments (e.g. auth)       |
|`update_jenkins_templates`  | false             | Updates the provided templates in the openshift namespace (as long as the user has permissions) and set's the default resource request/limits for the template |


OpenShift Version Compatibility
------------
When listing this role, make sure to pin the version of the role via one of the tags:

```
- src: siamaksade.openshift_jenkins
  version: 1.4.1
```  

The following tables shows the version combinations that are tested and verified:

|Role Version       | OpenShift Version |
|-------------------|-------------------|
| 1.0.x   | 3.7.x   |
| 1.1.x   | 3.9.x   |
| 1.2.x   | 3.10.x  |
| 1.3.x   | 3.11.x  |
| 1.4.x   | 3.11.x  |

__NOTE__: OCP 4.x samples operator will replace the Jenkins template after this role changes it, so that option will not work in OCP 4.x clusters with the sample operator enabled.

Note that if a version combination is not listed above, it does NOT mean that it won't work on that 
version. The above table is merely the combinations that we have verified and tested.


Example Playbook
------------

```
name: Example Playbook
hosts: localhost
tasks:
- import_role:
    name: siamaksade.openshift_jenkins
  vars:
    project_name: "cicd-project"
    openshift_cli: "oc --server http://master:8443"
```