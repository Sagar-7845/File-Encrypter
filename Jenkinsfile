node {
try {
stage('Build') {
sh '''
echo "Building Java project..."
echo "Listing workspace contents:"
ls
cd "Password Protection"
mkdir -p build
javac -d build src/*.java
echo "Build successful"
'''
}
stage('Test') {
 steps {
  sh '''
  echo "Running Test Stage..."

  cd "Password Protection"

  if [ -d "test" ]; then
      echo "Test folder found"

      rm -f junit-platform-console-standalone.jar

      curl -L -o junit-platform-console-standalone.jar \
      https://repo1.maven.org/maven2/org/junit/platform/junit-platform-console-standalone/1.10.0/junit-platform-console-standalone-1.10.0.jar

      mkdir -p test-build

      javac -cp junit-platform-console-standalone.jar:build \
      -d test-build test/*.java

      java -jar junit-platform-console-standalone.jar \
      --class-path build:test-build \
      --scan-class-path

  else
      echo "No test directory found — skipping tests"
  fi
  '''
 }
}
stage('Deploy') {
sh '''
echo "Deploying (Packaging) File-Encrypter Application..."
cd "Password Protection"
# Create executable artifact (JAR)
jar cf FileEncrypter.jar -C build .
echo "Deployment successful - Artifact ready"
'''
}
echo "Pipeline executed successfully!"
} catch (Exception e) {
echo "Pipeline failed!"
throw e
}
}
