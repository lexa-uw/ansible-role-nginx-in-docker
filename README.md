Run tests
=========

```bash
./tests/ops/bin/ansible ansible-galaxy install -r ./tests/requirements.yml --roles-path ./tests/roles/
./tests/ops/bin/ansible ansible-playbook tests/test.yml
```
