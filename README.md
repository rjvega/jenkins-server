# jenkins-server

Steps:
Create Centos VM and setup Jenkins
1. vagrant up
2. Point the browser to <vm-ip-addr>:8080 (See myipaddr.txt)
3. Login. Get the password from /var/lib/jenkins/secrets/initialAdminPassword
4. Click Install Suggested Plugin
5. Fill up the user fields
6. Click Start using Jenkins

Create sample project
7. Click Create new Jobs
8. Type Demo in the item name
9. Choose Freestyle project. Click OK
10. Go to Source Code Management tab, choose Git
11. Repository URL: https://github.com/rjvega/Angular2-Sample.git
12. Credentials: None
13. Go to Build tab, type "rm -rf node_modules"
14. Click Add build step. Type "npm install"
15. Click Apply. Click Save.

Build sample project
16. Click Build Now
