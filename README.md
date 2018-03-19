# The DevOPS Plan #
## 前言 ##
工具链  
|Type                   |Tool name  |Servers side   |Client side|VM name    |Dependence |
|:-:                    |:-:        |:-:            |:-:        |:-:        |:-:        |
|Planning Tools         |Jira       |y              |y          |CentPlan   |           |
|                       |Confluence |y              |           |CentPlan   |           |
|Source Code Management |GitLab     |y              |y          |CentSCM    |           |
|                       |Bitbucket  |y              |y          |CentSCM    |           |
|Continuous Development Tools   |Jenkins|y          |           |CentDev    |           |
|                       |Maven      |               |y          |CentDev    |           |
|                       |Nexus      |y              |y          |CentNexus  |           |
|Continuous Integration |SonarQube  |y              |y          |CentCI     |           |
|                       |Junit      |               |y          |CentDev    |           |
|                       |Tricentis  |y              |y          |           |           |
|Continuous delivery/deployment|Ansible|y           |y          |CentCD     |           |
|                       |Flyaway    |               |y          |CentDev    |           |
## 目录 ##
[1.CentOS配置](CentOS_configure.md)  
[2.安装MySQL](Install_MySQL.md)  
[3.安装SonarQube](Install_SonarQube.md)