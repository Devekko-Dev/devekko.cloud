
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