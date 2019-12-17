FROM dubheit/odoo-docker-image:12.0

USER root

# This will install the addons's python dependencies
COPY odoo-extra-requirements.txt odoo-extra-requirements.txt
RUN pip3 install -r odoo-extra-requirements.txt

USER odoo

ENV OCA_PATH /opt/odoo/oca
ENV EXTRAS_PATH /opt/odoo/extras
RUN mkdir -p $OCA_PATH $EXTRAS_PATH; \
rm -rf $OCA_PATH/*; \
rm -rf $EXTRAS_PATH/*; \ 
git clone --depth=1 -b 12.0 https://github.com/OCA/project.git $OCA_PATH/project; \
git clone --depth=1 -b 12.0 https://github.com/OCA/web.git $OCA_PATH/web; \
git clone --depth=1 -b 12.0 https://github.com/OCA/account-budgeting $OCA_PATH/account-budgeting;

COPY odoo_conf.yaml odoo_conf.yaml
RUN python3 scripts/generate_odoo_conf.py odoo.cfg.j2 odoo_conf.yaml > /opt/odoo/etc/odoo.cfg

RUN rm -rf /opt/odoo/.ssh
