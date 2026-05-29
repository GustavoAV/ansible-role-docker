create:
	vagrant up

apply:
	ansible-playbook -v ../setup.yml

apply_rootless:
	ansible-playbook -v ../setup.yml -e docker_enable_rootless_mode=true

clean:
	vagrant destroy -f

full:
	$(MAKE) clean
	@echo "[INFO] Testing rootful docker..."
	$(MAKE) create
	$(MAKE) apply
	$(MAKE) clean
	@echo "[INFO] Testing rootless docker"
	$(MAKE) create
	$(MAKE) apply_rootless
	$(MAKE) clean
