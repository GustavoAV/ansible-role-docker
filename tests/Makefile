BOX ?= cloud-image/ubuntu-26.04
OS_LIST := debian-12 debian-13 ubuntu-24.04 ubuntu-26.04 fedora-43 rocky-9 rocky-10
# OS_LIST := debian-12 debian-13 ubuntu-24.04 ubuntu-26.04

full: create apply clean

create:
	BOX="$(BOX)" vagrant destroy -f
	BOX="$(BOX)" vagrant up

apply:
	ansible-playbook -v ../setup.yml

clean:
	BOX="$(BOX)" vagrant destroy -f

get_boxes:
	$(foreach os, $(OS_LIST), vagrant box add --provider virtualbox "cloud-image/$(os)";)

full_all:
	@passed=""; \
	failed=""; \
	for os in $(OS_LIST); do \
		echo ""; \
		echo "========================================"; \
		echo "Testing: $$os"; \
		echo "========================================"; \
		if $(MAKE) full BOX="cloud-image/$$os"; then \
			passed="$$passed $$os"; \
			echo "✓ PASSED: $$os"; \
		else \
			failed="$$failed $$os"; \
			echo "✗ FAILED: $$os"; \
			$(MAKE) clean BOX="cloud-image/$$os" 2>/dev/null || true; \
		fi; \
	done; \
	echo ""; \
	echo "========================================"; \
	echo "SUMMARY"; \
	echo "========================================"; \
	echo "Passed:$$passed"; \
	echo "Failed:$$failed"; \
	echo ""; \
	if [ -z "$$failed" ]; then \
		echo "✓ All tests passed!"; \
		exit 0; \
	else \
		echo "✗ Some tests failed!"; \
		exit 1; \
	fi
