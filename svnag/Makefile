HOST=$(shell uname -n)

install:
	[ -d /root/.ssh ] || install -d -m 700 -o root -g root /root/.ssh
	grep svnag /root/.ssh/authorized_keys || echo 'command="/usr/local/sbin/svnag" ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAEAQDK6G/IZqUqN5nub/fd76eRMyMI0Ib/h5Hddp5Ppz1/YWUUpvqBPT3cfF2p+0UB69D9gQtcXLh35u8osIp8yfass3tnaaZb5fd2JNodDpgX+IdFMn6sE9tJLPo2PAaUexlO54sq0MgkGp0QzfaryKl1Ii3NbsPgJaPFhVQi8qC2cTf+wk/H8HaJVkCZ8MgzYTTN7fbiB0/QThJaAl3SL33e2ih55MCTEIIbPmx8is/jiXwguhUt+79mBEAc2wABmlWzzaEn7/LhVggofp2Bl2FwI5dpJeM+kEW6bUJdWZO6i31bH/EyX8GuCgdcsoGPPXBVBJrodkWSH+mWLGTi2PBzbSiJL/JY6cX1Kug59c7Zzb4hF8ciPnvs2piCYnVoajkKTNynqZwxZWy5imcSYmzrSooTABKm5dyHXl+hbbt9oAzR5ZuQgNTGbr9CUgqlWO9w+tLV8a7ooLwlD/eahXE1eE/uwiUZvrpbalu5LdJTL/rxXWeSJO2RjDnEISI2+VgmF45zT50JlsLZQUnRlt089msSx8sEYMAhhe4cqA2c+Upe8XmaVeytq9XRhw21JAafxD5WFHt8fL1b4GTiq9Yt3FVHD8UNqxnQ2KF9RfmBLVDX/+xEJdMRXTnRze//2O1J68tg7HXlyRNh5RU/510TltK9B/lgvsJu++TLP8GOhucTZnfdli+ZsuhAUQ68e1q+e5gJtZAcSa8kzWX+6Pl9X0nnfzD/H0fo/LcoEK8hSfjRlTijVoZ2/gB8WlXmGV+B/GeBt8eLzC/HMgh0z1FYUWhdvB0nUAcVkz1mTVUeierSTwTj26YIlHr83NPQbB0r5rJZE53g4qJTdMmUoMWAD5UzbdLNUnFL+o4EGIR0jbfHuOKHGw/hTEZhENGp6epSJ7bQr0a3u6fbA2KXWOKKwsdRNyP9+gGK2gDawnpZh8sEB+3bPk2aHQlbLbQf7ndLywibeb/zoJ6xBAjewMCyQF0LkE4VXvwPNphpegLLRVzVvUnHb1gOGjlFihJT8qLZl7o/LK3p8cQ9zCez0DM1Ol8tt4xwaf3uY9+ISmAp1baXaIlZyXoTy3PnjReghSKKIlJMq2LIJHBtD9ocLWK3fk2y0heh9cThzcYNChOwq5WRaXq+khjLjvUMEUHubn7P1mfIA34GrcwXLgH5LqJBVUk6Uk5c00ESfFpTsZAu4ycrBEmgLhDT5OE0NYs8JkXRKcA1JUPQgEfYYaEFFCh0WfpCb3YDZFY9037VsTH+y29sCcgBDBYVIhrioweM87PnLJabavMlLC+q29qGZwED4AX33wCO1dxn44+FodkrQrnLXwRMhPFugfMuh750h3qycEKuwWClSlG+ImjDWdjN svn@kirk' >>/root/.ssh/authorized_keys
	install -m 755 -o root -g root bin/svnag /usr/local/sbin/svnag
	[ -e cfg/$(HOST).cfg ] && install -m 644 -o root -g root cfg/$(HOST).cfg /etc/svnag.cfg \
		|| install -m 644 -o root -g root cfg/default.cfg /etc/svnag.cfg

dist:
	for i in $(notdir $(basename $(wildcard cfg/*.cfg))) ; do \
		[ "default" = "$$i" ] && continue ;\
		echo $$i ;\
		rsync -aHxC --delete ./ $$i:svnag/ ;\
	done

allinst:
	for i in $(notdir $(basename $(wildcard cfg/*.cfg))) ; do \
		[ "default" = "$$i" ] && continue ;\
		echo $$i ;\
		ssh -t $$i "su -c 'make -C /home/$$USER/svnag' -" |: ;\
	done
