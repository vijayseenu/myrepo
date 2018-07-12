# myrepo                                                  // Apache application deployment
---
- hosts: all                                              // To run this ansible script on all the hosts mentioned in the inventory
  tasks:                                                  // defining tasks what nees to be run on the client
  - name: Ensure apache is in latest version              // Description of the task performed
    yum: name=httpd state=latest                          // Make sure of httpd package is in the latest version
  - name: write apache config file                        // Description of the task performed
    template: src=/root/newhttpd.txt dest=/etc/httpd.conf // Source code in the host server /root and copying it to destination path
    notify:                                               // Handler functionality
    - restart apcahe                                      // Handler Name
  - name: ensure apache is running and enabled on boot    // Description of the task performed
    service:  name=httpd  state=started enabled=yes       // Starting the httpd service and enabling it on boot
  handlers:                                               // Ansible modules
    - name: restart apache                                // Handler Name
      service: name=httpd state=restarted                 // Restarting the httpd serivce 
