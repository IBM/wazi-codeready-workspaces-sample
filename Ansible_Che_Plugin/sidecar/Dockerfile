#
# Copyright IBM Corporation 2021
# This program and the accompanying materials are made
# available under the terms of the Eclipse Public License 2.0
# which is available at https://www.eclipse.org/legal/epl-2.0/
#
# SPDX-License-Identifier: EPL-2.0
#
# Contributors:
#   Red Hat, Inc. - base image and Che support
#   IBM Corporation - added "Red Hat Ansible Certified Content for IBM Z"
#

FROM quay.io/ansible/toolset:3.5.0

USER root

# Install z/OS collections from Ansible Galaxy
RUN ansible-galaxy collection install -p /usr/share/ansible/collections ibm.ibm_zos_core ibm.ibm_zos_ims ibm.ibm_zos_cics ibm.ibm_zhmc ibm.ibm_zos_sysauto

# add user, install ansible tools and preres such as openssh, apply permissions
RUN useradd -u 1000 -G root,root -d /home/wazi --shell /bin/bash -m wazi && \
    apt-get update && \
    apt-get -y install ansible-lint && \
    apt-get -y install openssh-client && \
    apt-get clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p ${HOME}/.ansible/tmp && \
    mkdir -p /projects && \
    mkdir -p /licenses && \
    for f in "/home/wazi" "/etc/passwd" "/etc/group" "/projects" "${HOME}/.ansible"; do\
        chgrp -R 0 ${f} && \
        chmod -R go+rwX ${f}; \
    done

# Add Profile
WORKDIR ${HOME}
COPY --chown=wazi:wazi profile.txt ${HOME}/.profile
RUN ln -sf ${HOME}/.profile ${HOME}/.bashrc && \
    chown -R wazi:wazi "${HOME}/.ansible"

# Wazi User
USER wazi
ADD etc/entrypoint.sh ${HOME}/entrypoint.sh
ENV SHELL=/bin/bash
ENTRYPOINT ["/home/wazi/entrypoint.sh"]

WORKDIR /projects
CMD tail -f /dev/null
