
asciinema rec demo1.cast

sh <(curl 'https://ash-hq.org/new/cloud?install=phoenix') \
    && cd cloud \
    && mix igniter.install \
    ash_phoenix ash_graphql ash_json_api ash_postgres \
    ash_sqlite ash_authentication ash_authentication_phoenix \
    ash_money ash_csv ash_admin ash_state_machine \
    ash_double_entry ash_archival ash_paper_trail cloak \
    ash_cloak \
    --auth-strategy password \
    --auth-strategy magic_link \
    --yes


 docker compose up cloud_pgvector_dev   


 Horizon install https://hexdocs.pm/horizon/readme.html


 mix horizon.init
Some releases have missing or nil configuration values.
Check `mix.exs` for missing config values or unset environment variables.
cloud: :build_host_ssh
cloud: :deploy_hosts_ssh
Created   bin/horizon_helpers.sh
Created   bin/stage-cloud.sh
Created   bin/build-cloud.sh
Created   bin/build_script-cloud.sh
Created   bin/deploy-cloud.sh
Created   bin/deploy_script-cloud.sh


ssh root@cloud "doas hostname cloud; doas sysrc hostname=cloud"
ssh root@cloud2 "doas hostname cloud2; doas sysrc hostname=cloud2"
ssh root@database "doas hostname database; doas sysrc hostname=database"
ssh root@database2 "doas hostname database2; doas sysrc hostname=database2"
ssh root@build "doas hostname build; doas sysrc hostname=build"

bsd_install.sh root@cloud web+proxy.conf


mix horizon.ops.init

 sh cloud/ops/bin/bsd_install.sh cloud horizon/web+proxy.conf


 Number of packages to be installed: 2

The process will require 9 MiB more space.
2 MiB to be downloaded.
[1/2] Fetching nginx-1.26.2_9,3.pkg: .......... done
[2/2] Fetching pcre2-10.43.pkg: .......... done
Checking integrity... done (0 conflicting)
[1/2] Installing pcre2-10.43...
[1/2] Extracting pcre2-10.43: .......... done
[2/2] Installing nginx-1.26.2_9,3...
===> Creating groups
Using existing group 'www'
===> Creating users
Using existing user 'www'
[2/2] Extracting nginx-1.26.2_9,3: .......... done
=====
Message from nginx-1.26.2_9,3:

--
Recent version of the NGINX introduces dynamic modules support.  In
FreeBSD ports tree this feature was enabled by default with the DSO
knob.  Several vendor's and third-party modules have been converted
to dynamic modules.  Unset the DSO knob builds an NGINX without
dynamic modules support.

To load a module at runtime, include the new `load_module'
directive in the main context, specifying the path to the shared
object file for the module, enclosed in quotation marks.  When you
reload the configuration or restart NGINX, the module is loaded in.
It is possible to specify a path relative to the source directory,
or a full path, please see
https://www.nginx.com/blog/dynamic-modules-nginx-1-9-11/ and
http://nginx.org/en/docs/ngx_core_module.html#load_module for
details.

Default path for the NGINX dynamic modules is

/usr/local/libexec/nginx.
[INFO] nginx installed successfully.
Updating PATH for nginx
nginx_enable:  -> YES
[INFO] nginx service enabled.
Performing sanity check on nginx configuration:
nginx: the configuration file /usr/local/etc/nginx/nginx.conf syntax is ok
nginx: configuration file /usr/local/etc/nginx/nginx.conf test is successful
Starting nginx.
[SUCCESS] [INFO] nginx service started.


bsd_install.sh admin@demo-pg1 postgres.conf



ssh admin@cloud "doas hostname cloud; doas sysrc hostname=cloud"
ssh admin@database "doas hostname database; doas sysrc hostname=database"
ssh admin@build "doas hostname build; doas sysrc hostname=build"
ssh admin@cloud2 "doas hostname cloud2; doas sysrc hostname=cloud2"
ssh admin@database2 "doas hostname database2; doas sysrc hostname=database2"


sh cloud/ops/bin/freebsd_setup.sh database
sh cloud/ops/bin/bsd_install.sh database horizon/postgres.conf


sh cloud/ops/bin/freebsd_setup.sh cloud
sh cloud/ops/bin/bsd_install.sh cloud horizon/web+proxy.conf


sh cloud/ops/bin/freebsd_setup.sh build
sh cloud/ops/bin/bsd_install.sh build horizon/build.conf


sh cloud/ops/bin/freebsd_setup.sh database2
sh cloud/ops/bin/bsd_install.sh database2 horizon/postgres-backup.conf


./ops/bin/bsd_install.sh admin@demo-pg2 postgres-backup.conf


chown -R admin:admin /home/admin



user = "admin"
host = "cloud"

projects = [
  %Horizon.Project{
    name: "cloud",
    server_names: ["cloud"],
    http_only: true,
    # certificate: :letsencrypt,
    # letsencrypt_domain: "cloud.folkbot.dev",
    servers: [
      # Verify PORT is same as in runtime.exs or env.sh.eex
      %Horizon.Server{internal_ip: "10.0.0.2", port: 4000},
      %Horizon.Server{internal_ip: "10.0.0.5", port: 4000}
    ]
  }
]


 IO.puts Horizon.NginxConfig.generate(projects)


 ./bin/stage-cloud.sh --force
 ./bin/build-cloud.sh --force

sh ./bin/stage-cloud.sh --force
sh ./bin/build-cloud.sh --force 