---
title: Configuring Git Large File Storage for your enterprise
intro: '{{ site.data.reusables.enterprise_site_admin_settings.configuring-large-file-storage-short-description }}'
redirect_from:
  - /enterprise/admin/guides/installation/configuring-git-large-file-storage-on-github-enterprise/
  - /enterprise/admin/installation/configuring-git-large-file-storage-on-github-enterprise-server
  - /enterprise/admin/installation/configuring-git-large-file-storage
  - /enterprise/admin/installation/configuring-git-large-file-storage-to-use-a-third-party-server
  - /enterprise/admin/installation/migrating-to-a-different-git-large-file-storage-server
  - /enterprise/admin/articles/configuring-git-large-file-storage-for-a-repository/
  - /enterprise/admin/articles/configuring-git-large-file-storage-for-every-repository-owned-by-a-user-account-or-organization/
  - /enterprise/admin/articles/configuring-git-large-file-storage-for-your-appliance/
  - /enterprise/admin/guides/installation/migrating-to-different-large-file-storage-server/
  - /enterprise/admin/user-management/configuring-git-large-file-storage-for-your-enterprise
versions:
  enterprise-server: '*'
---

### About {{ site.data.variables.large_files.product_name_long }}

{{ site.data.reusables.enterprise_site_admin_settings.configuring-large-file-storage-short-description }} You can use {{ site.data.variables.large_files.product_name_long }} with a single repository, all of your personal or organization repositories, or with every repository in {{ site.data.variables.product.product_location_enterprise }}. Before you can enable {{ site.data.variables.large_files.product_name_short }} for specific repositories or organizations, you need to enable {{ site.data.variables.large_files.product_name_short }} for your appliance.

{{ site.data.reusables.large_files.storage_assets_location }}
{{ site.data.reusables.large_files.rejected_pushes }}

For more information, see "[About {{ site.data.variables.large_files.product_name_long }}](/articles/about-git-large-file-storage)", "[Versioning large files](/enterprise/user/articles/versioning-large-files/)," and the [{{ site.data.variables.large_files.product_name_long }} project site](https://git-lfs.github.com/).

{{ site.data.reusables.large_files.can-include-lfs-objects-archives }}

### Configuring {{ site.data.variables.large_files.product_name_long }} for your appliance

{{ site.data.reusables.enterprise_site_admin_settings.access-settings }}
{{ site.data.reusables.enterprise_site_admin_settings.business }}
{% if currentVersion ver_gt "enterprise-server@2.21" %}
{{ site.data.reusables.enterprise-accounts.policies-tab }}
{% else %}
{{ site.data.reusables.enterprise-accounts.settings-tab }}
{% endif %}
{{ site.data.reusables.enterprise-accounts.options-tab }}
4. Under "{{ site.data.variables.large_files.product_name_short }} access", use the drop-down menu, and click **Enabled** or **Disabled**. ![Git LFS Access](/assets/images/enterprise/site-admin-settings/git-lfs-admin-center.png)

### Configuring {{ site.data.variables.large_files.product_name_long }} for an individual repository

{{ site.data.reusables.enterprise_site_admin_settings.override-policy }}

{{ site.data.reusables.enterprise_site_admin_settings.access-settings }}
{{ site.data.reusables.enterprise_site_admin_settings.repository-search }}
{{ site.data.reusables.enterprise_site_admin_settings.click-repo }}
{{ site.data.reusables.enterprise_site_admin_settings.admin-top-tab }}
{{ site.data.reusables.enterprise_site_admin_settings.admin-tab }}
{{ site.data.reusables.enterprise_site_admin_settings.git-lfs-toggle }}

### Configuring {{ site.data.variables.large_files.product_name_long }} for every repository owned by a user account or organization

{{ site.data.reusables.enterprise_site_admin_settings.access-settings }}
{{ site.data.reusables.enterprise_site_admin_settings.search-user-or-org }}
{{ site.data.reusables.enterprise_site_admin_settings.click-user-or-org }}
{{ site.data.reusables.enterprise_site_admin_settings.admin-top-tab }}
{{ site.data.reusables.enterprise_site_admin_settings.admin-tab }}
{{ site.data.reusables.enterprise_site_admin_settings.git-lfs-toggle }}

### Configuring Git Large File Storage to use a third party server

{{ site.data.reusables.large_files.storage_assets_location }}
{{ site.data.reusables.large_files.rejected_pushes }}

1. Disable {{ site.data.variables.large_files.product_name_short }} on the {{ site.data.variables.product.prodname_ghe_server }} appliance. For more information, see "[Configuring {{ site.data.variables.large_files.product_name_long }}](/enterprise/{{ currentVersion }}/admin/guides/installation/configuring-git-large-file-storage#configuring-git-large-file-storage-for-your-appliance)."

2. Create a {{ site.data.variables.large_files.product_name_short }} configuration file that points to the third party server.
  ```shell
  # Show default configuration
  $ git lfs env
  > git-lfs/1.1.0 (GitHub; darwin amd64; go 1.5.1; git 94d356c)
  > git version 2.7.4 (Apple Git-66)
  &nbsp;
  > Endpoint=https://<em>GITHUB-ENTERPRISE-HOST</em>/path/to/repo/info/lfs (auth=basic)
  &nbsp;
  # Create .lfsconfig that points to third party server.
  $ git config -f .lfsconfig remote.origin.lfsurl https://<em>THIRD-PARTY-LFS-SERVER</em>/path/to/repo
  $ git lfs env
  > git-lfs/1.1.0 (GitHub; darwin amd64; go 1.5.1; git 94d356c)
  > git version 2.7.4 (Apple Git-66)
  &nbsp;
  > Endpoint=https://<em>THIRD-PARTY-LFS-SERVER</em>/path/to/repo/info/lfs (auth=none)
  &nbsp;
  # Show the contents of .lfsconfig
  $ cat .lfsconfig
  [remote "origin"]
  lfsurl = https://<em>THIRD-PARTY-LFS-SERVER</em>/path/to/repo
  ```

3. To keep the same {{ site.data.variables.large_files.product_name_short }} configuration for each user, commit a custom `.lfsconfig` file to the repository.
  ```shell
  $ git add .lfsconfig
  $ git commit -m "Adding LFS config file"
  ```
3. Migrate any existing {{ site.data.variables.large_files.product_name_short }} assets. For more information, see "[Migrating to a different {{ site.data.variables.large_files.product_name_long }} server](#migrating-to-a-different-git-large-file-storage-server)."

### Migrating to a different Git Large File Storage server

Before migrating to a different {{ site.data.variables.large_files.product_name_long }} server, you must configure {{ site.data.variables.large_files.product_name_short }} to use a third party server. For more information, see "[Configuring {{ site.data.variables.large_files.product_name_long }} to use a third party server](#configuring-git-large-file-storage-to-use-a-third-party-server)."

1. Configure the repository with a second remote.
  ```shell
  $ git remote add <em>NEW-REMOTE</em> https://<em>NEW-REMOTE-HOSTNAME</em>/path/to/repo
  &nbsp;
  $ git lfs env
  > git-lfs/1.1.0 (GitHub; darwin amd64; go 1.5.1; git 94d356c)
  > git version 2.7.4 (Apple Git-66)
  &nbsp;
  > Endpoint=https://<em>GITHUB-ENTERPRISE-HOST</em>/path/to/repo/info/lfs (auth=basic)
  > Endpoint (<em>NEW-REMOTE</em>)=https://<em>NEW-REMOTE-HOSTNAME</em>/path/to/repo/info/lfs (auth=none)
  ```

2. Fetch all objects from the old remote.
  ```shell
  $ git lfs fetch origin --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Fetching objects...
  > Git LFS: (16 of 16 files) 48.71 MB / 48.85 MB
  ```

3. Push all objects to the new remote.
  ```shell
  $ git lfs push <em>NEW-REMOTE</em> --all
  > Scanning for all objects ever referenced...
  > ✔ 16 objects found
  > Pushing objects...
  > Git LFS: (16 of 16 files) 48.00 MB / 48.85 MB, 879.10 KB skipped
  ```

### 더 읽을거리

- [{{ site.data.variables.large_files.product_name_long }} project site](https://git-lfs.github.com/)