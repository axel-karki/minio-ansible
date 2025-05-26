## MinIO Setup

### What is MinIO?

**MinIO** is a high-performance, self-hosted object storage server that is fully compatible with the Amazon S3 API. It is ideal for storing application data, backups, and media in a scalable, cloud-native way.

---

## Installation

To install MinIO on a new VM, run:

```bash
ansible-playbook playbooks/install_minio.yml
```

This playbook:

* Installs MinIO as a systemd service
* Configures access and secret keys
* Sets up a data directory and default bucket

---

## Secure Configuration

Edit the following file to configure access credentials:

```bash
roles/minio/vars/main.yml
```

Recommended variables to set:

```yaml
minio_access_key: your access key
minio_secret_key: your secret key
```

**Encrypt the file using Ansible Vault:**

```bash
ansible-vault encrypt roles/minio/vars/main.yml
```

To edit securely later:

```bash
ansible-vault edit roles/minio/vars/main.yml
```

To run the playbook securely:

```bash
ansible-playbook playbooks/install_minio.yml --ask-vault-pass
```

Or using a password file:

```bash
ansible-playbook playbooks/install_minio.yml --vault-password-file ~/.vault_pass.txt
```

---

## Testing

After installation:

1. A test ClickHouse VM was configured to use MinIO for backups.

2. A test database and table were created:

<img width="404" alt="Screenshot 2025-05-26 at 6 54 53 AM" src="https://github.com/user-attachments/assets/9c9b7ac9-a2c8-4686-8269-4e9aac71d73d" />


3. A backup was created uploaded to MinIO using ansible:


4. The backup was successfully listed and verified in the MinIO UI under the configured bucket.

5. UI:
   ```
   ssh -i <ssh_file_path> -L 8080:<minio_vm_private_ip>:38773 root@<server_public_ip>
   ```
   <img width="919" alt="Screenshot 2025-05-26 at 6 56 48 AM" src="https://github.com/user-attachments/assets/b80f68b5-75af-4fd8-aad9-a66cb23757c4" />
<img width="977" alt="Screenshot 2025-05-26 at 6 59 31 AM" src="https://github.com/user-attachments/assets/aff77cc6-1537-455a-8b46-5c7bb9a4a580" />
   <img width="978" alt="Screenshot 2025-05-26 at 6 57 47 AM" src="https://github.com/user-attachments/assets/07b24838-9eee-4b46-86f7-ca9a05dcffaf" />
assets/91cdbb64-6a6b-4b34-8fee-804d5b6fa749" />
   <img width="973" alt="Screenshot 2025-05-26 at 6 58 08 AM" src="https://github.com/user-attachments/assets/eefc42e3-a16c-4727-b502-4e3a68b6959e" />


   
