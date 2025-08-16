FROM elasticsearch:7.17.26

# Copy the Tibetan Analyzer JAR into Elasticsearch
# COPY lucene-bo-1.5.0.jar /usr/share/elasticsearch/lib/
# Copy sysnonym file
COPY synonyms.txt /usr/share/elasticsearch/config/tibetan-synonyms.txt

COPY elasticsearch-analysis-tibetan-0.2.2-SNAPSHOT.zip /tmp/elasticsearch-analysis-tibetan-0.2.2-SNAPSHOT.zip
# Install the Tibetan Analyzer plugin
RUN elasticsearch-plugin install --batch file:///tmp/elasticsearch-analysis-tibetan-0.2.2-SNAPSHOT.zip

# Optional: clean up
RUN rm /tmp/elasticsearch-analysis-tibetan-0.2.2-SNAPSHOT.zip
