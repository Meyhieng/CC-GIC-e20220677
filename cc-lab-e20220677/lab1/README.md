
# Cloud Lab 1 Submission: Amazon EC2

- **Student name:** SAN Meyhieng
- **Student ID:** e20220677
- **Learner Lab user name:** Meyhieng
- **Date completed:** 23 Oct 2026

---

## Part 1.1: An Amazon EC2 Walkthrough

### Security group
![Security group](images/01-security-group.jpg)

### Key pair
![Key pair](images/02-key-pair.jpg)

### Instance details
![Instance details](images/03-instance-details.jpg)

### Browser test
![Browser test](images/04-browser-test.jpg)

### SSH connection
![SSH connection](images/05-ssh-connection.jpg)

---

## Part 1.2: Set Up an EC2 Web Solution (Challenge)

### Launch configuration
![Challenge launch](images/06-challenge-launch.jpg)

### Security group
![Challenge security group](images/07-challenge-security-group.jpg)

### Instance
![Challenge instance](images/08-challenge-instance.jpg)

### Commands I ran
```bash
ssh -i ~/.ssh/challenge-key-pair.pem ec2-user@ec2-35-170-201-38.compute-1.amazonaws.com
sudo dnf install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
echo "Welcome to the EC2 Challenge" | sudo tee /var/www/html/index.html
curl localhost
```

![Challenge terminal](images/09-challenge-terminal.jpg)

### Browser
![Challenge browser](images/10-challenge-browser.jpg)

---



