# ansible_playbook_Haproxy-update_from_configuration_file_dynamically_join_the_inventory_on_AWS

![1](https://user-images.githubusercontent.com/67523396/112658870-d8895d00-8e79-11eb-9879-84139c3c8f57.png)



HAProxy is free, open source software that provides a high availability load balancer and proxy server for TCP and HTTP-based applications that spreads requests across multiple servers. It is written in C and has a reputation for being fast and efficient.





As we are using ansible on top of AWS ,We need to configure the ansible configuration file .

![2](https://user-images.githubusercontent.com/67523396/112658877-da532080-8e79-11eb-8cae-6075167cd0e2.jpeg)



Here in my case I created a separate workspace where I kept all configuration file all yaml file ,So that it can be organised and easily used when needed .

![3](https://user-images.githubusercontent.com/67523396/112658878-da532080-8e79-11eb-95bd-4f3d1740da61.jpeg)


In ansible configuration file I also mentioned the private key for the ansible to do the authentication part very easily .

![4](https://user-images.githubusercontent.com/67523396/112658879-daebb700-8e79-11eb-96c2-5844e2cb6ce9.jpeg)
![5](https://user-images.githubusercontent.com/67523396/112658881-db844d80-8e79-11eb-9b77-5b2bfdceb8ab.jpeg)


Coming to the haproxy configuration file, which I would be sending from my controller node to all the managed node .
Here I used ‘for loop’ in Jinja language for printing Groups (apache) Value(Ip’s present in that group)

![6](https://user-images.githubusercontent.com/67523396/112658882-db844d80-8e79-11eb-9004-0108be7e3af9.jpeg)



I created the architecture in the type, like in future it would automatically update it’s configuration file on each time new Managed node join the inventory.

Let’s look onto the host file.

![7](https://user-images.githubusercontent.com/67523396/112658885-dc1ce400-8e79-11eb-831e-861efa55384c.jpeg)


Now when my playbook runs , It would automatically launch a webserver with a Load Balancer or Reverse proxy configured and also start the services .


![8](https://user-images.githubusercontent.com/67523396/112658887-dc1ce400-8e79-11eb-9cf8-b1901329e43f.jpeg)


After playbook runs ,explaining what is going on..

After running the Playbook ,It would first go to “apache” group in the inventory and in all those Ip’s go and launch Apache httpd Webserver and start the services.
Next step, It would now go to “haproxy” group in the inventory and then in that Ip it launches HAproxy and then copy the configuration file from controller node which would parse all the Ip’s from ‘apache” group and then update it to the managed Node ,Now it launches HAproxy services .

![9](https://user-images.githubusercontent.com/67523396/112658888-dcb57a80-8e79-11eb-8d4f-22e2ccf4a924.jpeg)


Finally, here is my small architecture on top of AWS which consist of a Load Balancer or Reverse Proxy at the Frontend and Apache Webserver at the backend .

![10](https://user-images.githubusercontent.com/67523396/112658890-dd4e1100-8e79-11eb-99ff-04b770ad56e7.jpeg)


After running ansible Playbook .

For demonstrating you all ,I changed the webpage with 1 and 2 ,So that you’ll can easily figure out reverse proxy is working .

![11](https://user-images.githubusercontent.com/67523396/112658891-dd4e1100-8e79-11eb-826d-346d49929450.jpeg)

![12](https://user-images.githubusercontent.com/67523396/112658893-dde6a780-8e79-11eb-9b64-8df8ff163c68.jpeg)


Open for any Query and Suggestions.

Thankyou






