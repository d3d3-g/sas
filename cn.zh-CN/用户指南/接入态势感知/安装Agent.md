# 安装Agent {#concept_dl4_ykc_zdb .concept}

态势感知Agent是态势感知提供的本地插件，您必须在服务器操作系统上安装态势感知Agent，才能使用态势感知提供的安全防护服务。

## 通过阿里云公共镜像自动安装 {#section_prp_z1d_zdb .section}

态势感知Agent已集成于阿里云公共镜像中。如果您在购买ECS实例时选择公共镜像，并选择启用**安全加固**，则态势感知Agent默认通过镜像安装。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13631/15349580864557_zh-CN.png)

## 查看服务器保护状态 {#section_izq_114_k2b .section}

您可以查看服务器的保护状态来确认态势感知Agent是否已安装及其在线/离线状态。

登录[云盾态势感知控制台](https://yundun.console.aliyun.com/?p=sas)，在资产列表页面查看所有服务器的**保护状态**：

-   **保护中**表示Agent已安装且处于在线状态。
-   **未受保护**表示Agent未安装或处于离线状态。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13631/15349580876339_zh-CN.jpg)

若您的服务器保护状态显示为**未受保护**，请按照以下方式，手动下载并安装态势感知Agent。

## 手动安装（支持非阿里云服务器） {#section_rrp_z1d_zdb .section}

**说明：** 如果您的服务器上安装了安全软件（如安全狗、云锁等），则态势感知Agent可能无法正常安装。在安装态势感知Agent前，请确认您的服务器上是否存在这类安全软件。如果存在，建议您暂时关闭或卸载该安全软件，然后再安装态势感知Agent。

**前提条件**

安装前，请确认您的服务器环境符合以下条件：

-   服务器在阿里云上，可以直接安装。
-   服务器不在阿里云上，与阿里云走Internet通信，应确保Internet连通。
-   服务器不在阿里云上，与阿里云通过专线连接走内网通信，则您需要在域名解析记录中添加以下DNS配置，指定态势感知服务端DNS：
    -   `100.100.25.3 jsrv.aegis.aliyun.com`
    -   `100.100.25.4 update.aegis.aliyun.com`

**操作步骤**

参照以下步骤，手动安装态势感知Agent：

1.  登录[云盾态势感知控制台](https://yundun.console.aliyun.com/?p=sas)。
2.  在左侧导航栏，单击**设置**。
3.  单击**安装/卸载插件**。
4.  根据服务器操作系统，选择对应安装步骤，获取并安装最新版本的态势感知Agent。
    -   **Windows系统**
        1.  在安装/卸载插件页面，单击**点击下载**，下载最新版本态势感知Agent安装文件到本地计算机。
        2.  将安装文件上传至您的Windows服务器。例如，您可以通过FTP工具，将安装文件上传到服务器。
        3.  在Windows服务器上，以管理员权限运行态势感知Agent安装程序，根据向导完成安装。

            **说明：** 态势感知Agent安装过程中，您会收到提示，要求您输入安装验证Key。该安装验证Key用于关联您的阿里云账号，您可在安装/卸载插件页面找到您的安装验证Key。

    -   **Linux系统**
        1.  根据实际情况，在态势感知Agent页面选择**阿里云服务器**或**非阿里云服务器**。
        2.  以管理员身份登录Linux服务器。
        3.  根据操作系统类型，选择32位或64位的安装命令，并复制至Linux服务器上。
        4.  执行安装命令，完成态势感知Agent的下载及安装。

            **说明：** 该安装命令包含从阿里云站点下载最新版本的态势感知Agent，请确认您的服务器已连接公网。

5.  态势感知Agent安装完成约五分钟后，您可以在云盾态势感知控制台资产列表页，查看服务器的保护状态：
    -   阿里云服务器会从**未受保护**变成**保护中**。
    -   非阿里云服务器会被添加至服务器列表。

## 验证Agent安装 {#section_csp_z1d_zdb .section}

成功安装态势感知Agent后，建议您参照以下步骤进行验证：

1.  检查您的服务器上态势感知Agent的AliYunDun和AliYunDunUpdate进程是否正常运行。关于态势感知Agent进程说明，请参考[Agent说明](intl.zh-CN/用户指南/接入态势感知/Agent说明.md#)。
2.  在您的服务器上执行以下telnet命令，检查您的服务器是否能正常连通态势感知服务器：

    **说明：** 确保您的服务器能够连通至少一个jsrv和一个update服务域名。

    -   `telnet jsrv.aegis.aliyun.com 80`
    -   `telnet jsrv2.aegis.aliyun.com 80`
    -   `telnet jsrv3.aegis.aliyun.com 80`
    -   `telnet update.aegis.aliyun.com 80`
    -   `telnet update2.aegis.aliyun.com 80`
    -   `telnet update3.aegis.aliyun.com 80`

如果态势感知Agent安装验证失败，请参考[Agent离线排查](intl.zh-CN/用户指南/接入态势感知/Agent离线排查.md#)。

## 注意事项 {#section_fsp_z1d_zdb .section}

非阿里云服务器必须通过安装程序（Windows）或脚本命令（Linux）安装态势感知Agent。

如果您的非阿里云服务器通过以下方式安装态势感知Agent，则您需要删除态势感知Agent目录后，按照上述手动安装步骤重新安装态势感知Agent。

-   通过已安装态势感知Agent的镜像批量安装服务器。
-   从已安装态势感知Agent的服务器上直接复制态势感知Agent文件。

**态势感知Agent文件目录**

-   Windows：C:\\Program Files \(x86\)\\Alibaba\\Aegis
-   Linux：/usr/local/aegis

