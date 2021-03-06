# Implementation of a Secure Engineering Process for Open Source Projects

This intern project aims to address the security issues present in many open source projects. In particular, this document will be targeted towards the Open Source Software Defined Networking stack, OpenDaylight (ODL). 

Please see the following [link](https://wiki.opendaylight.org/view/InternProjects:Main#Implement_a_secure_engineering_process_for_OpenDaylight) for more details on this project: 

## Best Practices for Secure Development in Open Source

The following guide will be focued towards secure development flow. For bug patching procedures please see, [link](https://wiki.opendaylight.org/view/Life_Cycle_of_a_Bug) and [instructions](https://wiki.opendaylight.org/view/TSC:Vulnerability_Management) for vulnerability management, ODL security response team.

### Common Practices in Secure Development
1. Training for developers/operators
2. Specific testing procedures and testers
3. Continuous Integration (CI) testing and standards enforcement
4. Best Practices documentation

## Current ODL Development Lifecycle
1. Gerrit             (Source Code Management)
2. Jenkins            (Continuous Integration Build Server)
2. Bugzilla           (Bug Tracking)
3. Sonar Qube         (Quality Control)

## Issues of process adoption
1. Scalability
2. Ease of Integration

__General Issues of Open Source__

Open source projects require management of people from a wide variety of skill sets and timezones. Therefore, some of the main issues to adoption of security processes are scability and ease of adoption. Considering this, training and manual testing procedures are difficult to implement and scale for open source projects. CI servers are usually implemented as part of the build process, so tools such as static code analysis can be easily implmented, but add a level of assurance. 

## Proposed Integration of Tools
1.Dependency Management

Large scale software projects nowadays involve large amount of code written outside the project itself. Therefore, vulnerabilites in dependant libararies can cause security issues if not updated quickly. Nested dependencies however, can make it difficult to trace the problematic dependency as the same libary may be used more than once, with different versions. 

A proposed tool is [OWASP_dependency_check](https://wiki.jenkins-ci.org/display/JENKINS/OWASP+Dependency-Check+Plugin), that has both a maven and jenkins plugin. Furthermore, the tool checks for vulnerable software against data from the NVD (National Vulnerability Database). In order to address False Positives, an xml file can be specified to supress results in a scan. 

![alt tag](https://raw.github.com/willtmwu/SecureEngineeringProcess_OpenSource/master/pictures/Dependency_Findbugs.png)

2.Static Code Analysis

Common security problems can often arise from simple mistakes in code and slip through a peer review system such as Gerrit. This issue can be addressed by scanners that identify potentially problematic code. However, no tool is completely free of false positives/negatives. A possible way that this could be addressed is a workflow that allows experienced developers/operators to select which issues are false positives. These false issues are then stored and persistent across builds.  

The tool [find-sec-bugs](https://github.com/h3xstream/find-sec-bugs) is a findbugs plugin that utilises static analysis to scan code for common code security vulnerabilities. A plugin for maven and jenkins allows for quick viewing of trends in the build screen. As the findbugs tool is able to determine the line of code that the issues occurs, the false positive workflow will be able store the code, line number and issue.

![alt tag](https://raw.github.com/willtmwu/SecureEngineeringProcess_OpenSource/master/pictures/False_positive_workflow.png)
