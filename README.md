感谢 P3TERX/Actions-OpenWrt和coolsnowwolf/lede

通过创建流程文件，在线编译helloworld服务固件；

第一代passwall源码完全停止开发(开源源码已经移除)，基于vuejs脚本语言、焕新UI设计的第二代passwall由Lienol等大神们在私有库闭源开发中，看情况和心情，只有极小可能性以后某天开源，不要过分期待。

修改流程文件REPO_URL: 不同库地址（默认lean的https://github.com/coolsnowwolf/lede.git或Lienol的https://github.com/Lienol/openwrt）；REPO_BRANCH: 不同分支 （以Lienol OpenWrt源码为例分支dev-master 激进；dev-19.07 OpenWrt官方平稳版；dev-lean-lede lean的源码）。

通过修改diy-part1.sh文件修改feeds.conf.default配置。默认添加fw876/helloworld。
有能力可以添加包含passwall的lienol-openwrt-package试试。

通过修改diy-part2.sh文件可以自定义默认IP，登陆密码等。按我的需要现在的默认IP为192.168.1.11

修改流程触发条件。默认添加两种触发方式：
“Webhook”（给 GitHub API 发送一个 repository dispatch event(仓库调度事件) 请求，当 API 接收到请求后就会触发相应的 workflow）
以下是一个使用 cURL 发送请求的例子：
curl -X POST https://api.github.com/repos/:owner/:repo/dispatches \
-H "Accept: application/vnd.github.everest-preview+json" \
-H "Authorization: token ACTIONS_TRIGGER_TOKEN" \
--data '{"event_type": "TRIGGER_KEYWORDS"}'
需要要替换的值：
:owner- 用户名
:repo - 需要触发的 Github Action 所在的仓库名称
ACTIONS_TRIGGER_TOKEN - 带有 repo 权限的 Personal access token
TRIGGER_KEYWORDS - 自定义 Webhook 事件名称，可以为任意值，Actions 列表中会显示此名称。
“Star”（点击仓库上的 Star 按钮即可触发 GitHub Actions的工作流程，为了避免被其他人点击 Star 导致的不必要的麻烦，只有仓库所有者，也就是你自己点 Star 才有效）。

在触发工作流程后，默认SSH_ACTIONS: true在 Actions 页面等待执行到SSH connection to Actions步骤，会出现下面信息：

To connect to this session copy-n-paste the following into a terminal or browser:

ssh Y26QeagDtsPXp2mT6me5cnMRd@nyc1.tmate.io

https://tmate.io/t/Y26QeagDtsPXp2mT6me5cnMRd

复制 SSH 连接命令粘贴到终端内执行，或者复制链接在浏览器中打开使用网页终端，登陆云menuconfig。

命令：cd openwrt && make menuconfig

新手参考OpenWrt MenuConfig设置和LuCI插件选项说明

完成后按快捷键Ctrl+D或执行exit命令退出，后续编译工作将自动进行。

这样比较灵活，可以根据路由器硬件通过云menuconfig自定义配置固件，不需要再导出.config和上传

进阶玩法请看P3TERX的博客中文教程

使用同步.config多流程编译移步Actions-Lean-OpenWrt
# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Stars&logo=github)
![GitHub Forks](https://img.shields.io/github/forks/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Forks&logo=github)

Build OpenWrt using GitHub Actions

[Read the details in my blog (in Chinese) | 中文教程](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

## Usage

- Click the [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) button to create a new repository.
- Generate `.config` files using [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) source code. ( You can change it through environment variables in the workflow file. )
- Push `.config` file to the GitHub repository.
- Select `Build OpenWrt` on the Actions page.
- Click the `Run workflow` button.
- When the build is complete, click the `Artifacts` button in the upper right corner of the Actions page to download the binaries.

## Tips

- It may take a long time to create a `.config` file and build the OpenWrt firmware. Thus, before create repository to build your own firmware, you may check out if others have already built it which meet your needs by simply [search `Actions-Openwrt` in GitHub](https://github.com/search?q=Actions-openwrt).
- Add some meta info of your built firmware (such as firmware architecture and installed packages) to your repository introduction, this will save others' time.

## Acknowledgments

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © P3TERX
