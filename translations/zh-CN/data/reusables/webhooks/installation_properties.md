| 键        | 类型    | 描述                                                               |
| -------- | ----- | ---------------------------------------------------------------- |
| `action` | `字符串` | 执行的操作内容. 可以是以下选项之一：<ul><li>`created` - Someone installs a {{ site.data.variables.product.prodname_github_app }}.</li><li>`deleted` - Someone uninstalls a {{ site.data.variables.product.prodname_github_app }}</li>{% if currentVersion == "free-pro-team@latest" or currentVersion ver_gt "enterprise-server@2.20" %}<li>`suspend` - Someone suspends a {{ site.data.variables.product.prodname_github_app }} installation.</li><li>`unsuspend` - Someone unsuspends a {{ site.data.variables.product.prodname_github_app }} installation.</li>{% endif %}<li>`new_permissions_accepted` - Someone accepts new permissions for a {{ site.data.variables.product.prodname_github_app }} installation. When a {{ site.data.variables.product.prodname_github_app }} owner requests new permissions, the person who installed the {{ site.data.variables.product.prodname_github_app }} must accept the new permissions request. </li></ul>                     |
| `仓库`     | `数组`  | An array of repository objects that the insatllation can access. |