## Debian

######Installing Oracle Java:
  1. List the java that is currently in use:
  `# update-alternatives --display javac`
  2. `# mkdir /opt/oracle-jdk7`
  3. `# tar -zxf jdk-7*.tar.gz -C /opt/java-oracle/`
  4. `# update-alternatives --install /usr/bin/java java /opt/java-oracle/jdk1.X.X_XX/bin/java 20000`
  5. `# update-alternatives --install /usr/bin/javac javac /opt/java-oracle/jdkX.X._XX/bin/javac 20000`
  6. `# update-alternatives --config java`
