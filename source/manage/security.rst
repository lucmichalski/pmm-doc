########
Security
########

************
Introduction
************

You can protect from unauthorized access to Percona Monitoring and Management by using:

- SSL encryption to secure traffic between PMM server and client components;
- Strong passwords for adminstrator and user accounts in the web interface.

Additional measures include:

- Where possible, using isolation, running your server as a container or virtual machine;

- Ensuring all components are working within a firewalled environment;

- With Docker, restricting PMM Server connections to port 443 by using a single publish option: ``--publish=443:443``;

- Using a separate network for PMM communications.

******************
Traffic encryption
******************

Clients and servers can communicate via SSL if signed certificates are installed.

Virtual and container images (Docker, OVF and AMI) come with self-signed certificates.

Use ``pmm-admin`` to configure clients to use SSL and a certificate from a Certificate Authority.

.. code-block:: bash

   pmm-admin config --server <server IP/hostname> --server-ssl

For self-signed certificates:

.. code-block:: bash

    pmm-admin config --server <server IP/hostname> --server-insecure-ssl

With Docker, certificates can be either mounted or copied into the container.

1. Mount the certificates directory and only using port 443.

    The certificate files in ``/etc/pmm-certs``:

    - ``certificate.crt``
    - ``certificate.key``
    - ``ca-certs.pem``
    - ``dhparam.pem``

    In this example, certificates are in ``/etc/pmm-certs`` and mounted in the container to ``/srv/nginx``.

    .. code-block:: bash

       docker run -d -p 443:443 \
       --volumes-from pmm-data \
       --name pmm-server \
       -v /etc/pmm-certs:/srv/nginx \
       --restart always \
       percona/pmm-server:2

2. Copy certificates inside the container.

    .. code-block:: bash

       docker cp certificate.crt pmm-server:/srv/nginx/certificate.crt
       docker cp certificate.key pmm-server:/srv/nginx/certificate.key
       docker cp ca-certs.pem pmm-server:/srv/nginx/ca-certs.pem
       docker cp dhparam.pem pmm-server:/srv/nginx/dhparam.pem



*********
Passwords
*********

Choose strong passwords when:

- first logging into PMM and changing the default administrator's password -- do not skip this step;

- when creating users via *Configuration > Users*.

Additional measures:

- Do not allow your browser to store passwords when logging into the web interface.
- Implement password strength checking and password change schedules.

*******
Backups
*******

Backups of pmm-data Docker containers should be encrypted or stored in secure location.

**********************
Logging and Monitoring
**********************

- Monitor web server logs to detect unauthorized logins.
- Keep web server logs secure through correct filesystem permissioning and ownership settings.