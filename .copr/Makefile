.PHONY: srpm

srpm:
	dnf -y install curl rpm-build
	version="$$(rpmspec -q --qf '%{version}\n' "$(spec)" | head -n1)"; \
	mkdir -p "$(outdir)"; \
	curl --fail --location --retry 3 \
	  --output "$(outdir)/v$${version}.tar.gz" \
	  "https://github.com/wayvr-org/wayvr/archive/refs/tags/v$${version}.tar.gz"; \
	curl --fail --location --retry 3 \
	  --output "$(outdir)/vendor.tar.xz" \
	  "https://github.com/wayvr-org/wayvr/releases/download/v$${version}/vendor.tar.xz"; \
	rpmbuild -bs "$(spec)" \
	  --define "_sourcedir $(outdir)" \
	  --define "_srcrpmdir $(outdir)"
