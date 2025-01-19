
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