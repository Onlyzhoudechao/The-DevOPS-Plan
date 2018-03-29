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
|                       |Tricentis  |y              |y           |           |           |
|Continuous delivery/deployment|Ansible|y           |y          |CentCD     |           |
|                       |Flyaway    |               |y          |CentDev    |           |


</br>
</br>

********************************
## 目录 ##
[1.CentOS配置](CentOS_configure.md)  
[2.安装MySQL](Install_MySQL.md)  
[3.安装SonarQube](Install_SonarQube.md)  
[4.安装Bitbucket](Install_bitbucket.md)  
[5.安装gitlab](Install_gitlab.md)  
[6.安装nexus](Install_nexus.md)  
[7.安装maven](install_maven.md)  
[8.安装tomcat](install_tomcat.md)  
[9.安装ansible](Install_ansible.md)  
[10.Jenkins与Jira集成](Jenkins_integrate_with_Jira.md)  
</br>
</br>    
    
[**最佳实践V1**](Tool-chain-v1.md)