OVN_VERSION 	:= 20.09.0
OVS_VERSION 	:= 2.14.0

.PHONY: srpm
srpm:
	curl -s -L https://github.com/ovn-org/ovn/archive/v$(OVN_VERSION).tar.gz -o rpmbuild/SOURCES/ovn-$(OVN_VERSION).tar.gz
	curl -s -L https://github.com/openvswitch/ovs/archive/v$(OVS_VERSION).tar.gz -o rpmbuild/SOURCES/openvswitch-$(OVS_VERSION).tar.gz
	mkdir -p ovn-$(OVN_VERSION)/openvswitch-$(OVS_VERSION)
	tar xf rpmbuild/SOURCES/ovn-$(OVN_VERSION).tar.gz --strip 1 -C ovn-$(OVN_VERSION)
	tar xf rpmbuild/SOURCES/openvswitch-$(OVS_VERSION).tar.gz --strip 1 -C ovn-$(OVN_VERSION)/openvswitch-$(OVS_VERSION)
	tar czf rpmbuild/SOURCES/ovn-$(OVN_VERSION).tar.gz ovn-$(OVN_VERSION)
	rm -rf ovn-$(OVN_VERSION)
	dnf install -y 'dnf-command(builddep)'
	dnf builddep -y $(spec)
	rpmbuild --without check \
            -D'_srcrpmdir $(outdir)' \
            -D'_topdir $(shell pwd)/rpmbuild' -ba $(spec)
