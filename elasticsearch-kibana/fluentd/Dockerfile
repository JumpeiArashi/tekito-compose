FROM fluent/fluentd:latest-onbuild
USER fluent
WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.3.0/bin:$PATH
RUN mkdir -p /home/fluent/logs
RUN gem install fluent-plugin-elasticsearch
ADD fluent.conf /home/fluent/fluent.conf 
CMD fluentd -v -c /home/fluent/fluent.conf -p /fluentd/plugins $FLUENTD_OPT
