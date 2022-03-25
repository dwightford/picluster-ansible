# picluster-ansible



# FOR-DEVS

- The idea is to make it as simple possible to create a function that is built for, deployed to and run on Docker Swarm or Kubernetes, while providing a workflow that integrates directly with the Docker ecosystem. Rather than throwing a zip file over a wall or editing in a web-form they can actually go ahead and build a Docker image from GitHub and then use the same artifact in dev, staging and production. 

By building on top of a container orchestration platform, you get a lot of built-in functionality such as self-healing infrastructure, auto-scaling and the ability to control every aspect of the cluster.


To run the playbook I issue the following command from my picluster-ansible repository project directory:

</a>.
$ ansible-playbook up.yml -i inventory.yml

This will update all software packages and install all the monitoring exporter tools on each Raspberry Pi host (as defined in the inventory.yml file). There is a separate section for the installation of the monitoring software (Prometheus and Grafana) which is applied only to the host defined as the monitoring_server in the inventory.yml file.

For details on the actual tasks involved in provisioning the hosts please explore the GitHub repository.

# Prometheus

After running the up.yml Ansible playbook I have Prometheus installed and running, as well as the exporter tools running on each Pi. This can be verified by visiting the 

Prometheus web UI running on my monitoring_server host at http://na0.local:9090. Using the RPi Exporter I can use the web UI directly to view the current temperature measurements using the query rpi_cpu_temperature_celsius:


# Grafana
While Prometheus does have the ability to display and even graph exported measurements, there are much better tools for this job. Grafana is an open source metrics visualisation tool which I am using to create dashboards for my Pi cluster.

Grafana was installed with the up.yml Ansible playbook, and can be accessed on the monitoring_server host on port 3030: http://na0.local:3030. While Grafana can take some time to become familiar with, it essentially allows for a collection of “panels” to be grouped together as a dashboard. Grafana supports multiple data sources, one of which is Prometheus. After logging in and changing the default admin password I selected Prometheus as a data source for Grafana: