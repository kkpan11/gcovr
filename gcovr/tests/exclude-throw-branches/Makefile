all:
	$(CXX) -fprofile-arcs -ftest-coverage -fPIC main.cpp -o testcase

run: json txt cobertura html sonarqube jacoco coveralls

coverage-throw.json coverage-excl-throw.json:
	./testcase
	$(GCOVR) --gcov-keep --json-pretty --json coverage-throw.json
	$(GCOVR) --gcov-keep  --json-pretty --json coverage-excl-throw.json --exclude-throw-branches

json: coverage-throw.json coverage-excl-throw.json
	echo "Files created"

txt: coverage-throw.json coverage-excl-throw.json
	$(GCOVR) -a coverage-throw.json -o coverage-throw.txt
	$(GCOVR) -a coverage-excl-throw.json -o coverage-excl-throw.txt

cobertura: coverage-throw.json coverage-excl-throw.json
	$(GCOVR) -x -a coverage-throw.json -o cobertura-throw.xml
	$(GCOVR) -x -a coverage-excl-throw.json -o cobertura-excl-throw.xml

html: coverage-throw.json coverage-excl-throw.json
	$(GCOVR) --html-details -a coverage-throw.json -o coverage-throw.html
	$(GCOVR) --html-details -a coverage-excl-throw.json -o coverage-excl-throw.html

sonarqube: coverage-throw.json coverage-excl-throw.json
	$(GCOVR) --sonarqube -a coverage-throw.json -o sonarqube-throw.xml
	$(GCOVR) --sonarqube -a coverage-excl-throw.json -o sonarqube-excl-throw.xml

jacoco: coverage-throw.json coverage-excl-throw.json
	$(GCOVR) --jacoco -a coverage-throw.json -o jacoco-throw.xml
	$(GCOVR) --jacoco -a coverage-excl-throw.json -o jacoco-excl-throw.xml

coveralls: coverage-throw.json coverage-excl-throw.json
	$(GCOVR) --coveralls-pretty --coveralls -a coverage-throw.json -o coveralls-throw.json
	$(GCOVR) --coveralls-pretty --coveralls -a coverage-excl-throw.json -o coveralls-excl-throw.json

clean:
	rm -f testcase
	rm -f *.gc*
	rm -f coverage*.* cobertura*.* sonarqube*.* jacoco*.* coveralls-*.json
