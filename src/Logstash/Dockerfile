FROM debian:latest

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y gpg
RUN apt-get install -y vim

RUN wget -qO- https://artifacts.elastic.co/GPG-KEY-elasticsearch | gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

RUN echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | tee /etc/apt/sources.list.d/elastic-8.x.list

RUN apt-get update
RUN apt-get install logstash

COPY logstash.conf /etc/logstash/conf.d/
COPY ilm-setup.txt /etc/logstash/ilm-setup.txt

ENV PATH=/usr/share/logstash/bin:$PATH

RUN logstash-plugin install logstash-filter-environment
RUN mkdir /etc/logstash/ssl

CMD ["logstash", "--path.settings=/etc/logstash", "--config.reload.automatic"]