# How-to-run-GitLab-in-a-docker-container

> Install Docker engine
> Pull “GitLab” docker image from docker hub
> Run “GitLab” docker container
> Create a sample project in GitLab
> Work with “git” command line
> Take a backup of GitLab
> Restore GitLab from the backup


STEP-1: Install and start docker engine

	yum install docker

	systemctl start docker

	systemctl enable docker

	systemctl status docker



STEP-2: Pull and run GitLab docker image

	docker search gitlab

	docker pull docker.io/gitlab/gitlab-ce

	docker images

	docker run -d --hostname gitlab-sunil.simplylearn.com \
	-p 443:443 -p 80:80 -p 2222:22 \
	--name gitlab-sunil \
	--restart unless-stopped \
	--volume /storage/gitlab/config:/etc/gitlab \
	--volume /storage/gitlab/logs:/var/log/gitlab \
	--volume /storage/gitlab/data:/var/opt/gitlab \
	gitlab/gitlab-ce:latest

	docker ps

	docker logs <48b0bfecd627> -f



STEP-3: Login GitLab and create a new project

	URL: http://gitlab-sunil.simplylearn.com>

	Create password for Administrator(root)

	Login with the updated credentials and create a new project



STEP-4: Work with some git command line

	git config --global user.name "Administrator"

	git config --global user.email "admin@example.com"

	git clone http://gitlab-sunil.simplylearn.com/root/my_first_project.git

	cd my_first_project

	touch README.md

	git add README.md

	git commit -m "add README"

	git push -u origin master



STEP-4: Backup and Restore of GitLab

	/usr/bin/docker exec -i gitlab-sunil /opt/gitlab/bin/gitlab-rake \
	gitlab:backup:create

	crontab -l
		0 7 * * * <COMMAND>

	docker exec -it gitlab-sunil ls /var/opt/gitlab/backups/

	docker exec -it gitlab-sunil /opt/gitlab/bin/gitlab-rake \
	gitlab:backup:restore BACKUP=<1492443013_2019_03_05>
  
  
