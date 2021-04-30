![Lifecycle:Stable](https://img.shields.io/badge/Lifecycle-Stable-97ca00)


# Migration Playbook

1. Copy `inventory.sample` to `inventory` and fill in the values for which cluster you want to talk to an yhour login names/tokens

2. Run the playbook.

   ```bash
   $ ansible-playbook -i inventory migrate.yaml -e "plan=capstone key=xordpe"
   ```
