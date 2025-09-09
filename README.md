---
- name: Launch EC2 instance
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
    region: us-east-1
    instance_type: t2.micro
    ami_id: ami-00ca32bbc84273381
    key_name: server-key  #give name of your existing key_pair thats downloaded in your localmachine
    security_group: my-sg  #same sg name with what you created your instance

  tasks:
    - name: Launch instance
      amazon.aws.ec2_instance:
        name: ansible-new-server
        key_name: "{{ key_name }}"
        instance_type: "{{ instance_type }}"
        image_id: "{{ ami_id }}"
        wait: yes
        region: "{{ region }}"
        security_group: "{{ security_group }}"
        count: 1
        network:
          assign_public_ip: true
        tags:
          Environment: Devops
...           
