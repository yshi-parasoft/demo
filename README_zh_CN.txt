���ڶ� Ant��Maven �� Gradle ���ɵ���������������·����ȡ:
https://docs.parasoft.com/display/JTEST20242/Integrating+with+Build+Systems

���ĵ����������ʹ�� Jtest ִ�о�̬���������в����Լ��ռ�
��������Ϣ - ʹ�ò�Ʒ�и����� "demo" ��Ŀ��

��ע�⣬����Ŀ�ķ�����ʹ�� demo.properties �ļ���ָ��
���������õġ����ļ�λ�� [INSTALL]/examples/demo Ŀ¼�С�

PowerShell �û���ע��:
���� PowerShell ���������ַ��ķ�ʽ�����������а������ǰ�����ۺŵĲ�����ʱ���ܻᵼ��������Ϊ��
Ϊȷ��˳��ִ�У���ʹ�����·���֮һ:
A.  ʹ�÷����� "`" ������ǰ�����ۺš�
    ʾ��:
    `-Djtest.config="builtin://Demo Configuration"

B.  ��˫���Ž���������ֵ��������
    ʾ��:
    "-Djtest.config=builtin://Demo Configuration"


ǰ������
-------------------------------------------------
1. �� Jtest ��װĿ¼�е� jtestcli.properties �ļ������� Jtest ���֤��


Jtest �����ļ�
-------------------------------------------------
1. ���� "Recommended Rules" �������ã���ֱ��ִ�о�̬���� (�����κι���ϵͳ) - ʹ����������:
   Windows:
     ..\..\jtestcli.exe -config "builtin://Recommended Rules" -data demo.data.json -report report
   UNIX:
     ../../jtestcli -config "builtin://Recommended Rules" -data demo.data.json -report report


Ant
-------------------------------------------------
1. ��ȷ������·���ϴ��ڿ��õ� "ant"��

2. ���� "Demo Configuration"����ִ�о�̬���������ռ���Ԫ���Եĸ�����:

     ant -file jtest.xml -Djtest.config="builtin://Demo Configuration"

   ������ "demo" ��Ŀ�����е�Ԫ���ԡ�Ant �� Jtest ����ռ�Դ����������ݺͰ��������ʵĵ�Ԫ���Խ������ִ�з��������ɱ��档

   ע�⣺

   �������о�̬��������ʹ����������:

     ant -file jtest.xml jtest-sae

   �������е�Ԫ���ԣ���ʹ����������:

     ant -file jtest.xml jtest-utc

   jtest.xml ��ָ�������� - ����� "jtest"��"jtest-sae" �� "jtest-utc" Ŀ�ꡣ


Maven
-------------------------------------------------
1. ����� Jtest �û�ָ���������� Maven ����:
   https://docs.parasoft.com/display/JTEST20242/Configuring+the+Jtest+Plugin+for+Maven

2. ���� "Demo Configuration" ��ִ�о�̬���������ռ����ڵ�Ԫ���Եĸ�����:

     mvnw  clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Demo Configuration"

   ������ "demo" ��Ŀ�������е�Ԫ���ԡ�Maven �� Jtest ����ռ�Դ����������ݺ�
   ���������ʵĲ��Խ������ִ�з��������ɱ��档

   ע�⣺

   �������о�̬��������ʹ����������:

     mvnw jtest:jtest

   Ĭ��ʹ�� "Recommended Rules" �������á�

   �������е�Ԫ���ԣ���ʹ����������:

     mvnw clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Unit Tests"


Gradle
-------------------------------------------------
ע��: ���� "demo" ��Ŀʹ�� JUnit 5, ��Ҫ Gradle 4.6 ����߰汾��

1. ������ Jtest ��װ��������������õ������ű��� "jtest" �顣

2. ���� "Demo Configuration"����ִ�о�̬���������ռ����ڵ�Ԫ���Եĸ�����:

     gradlew clean jtest-agent test jtest -Djtest.config="builtin://Demo Configuration"

   ������ "demo" ��Ŀ�������е�Ԫ���ԡ�Gradle �� Jtest ������ռ�Դ����������ݺͲ��Խ������ִ�к����ɱ��档

   ע��:

   �������о�̬��������ʹ����������:

     gradlew clean assemble jtest

   Ĭ��ʹ�� "Recommended Rules" ���á�

   �������е�Ԫ���ԣ���ʹ����������:

     gradlew clean jtest-agent test jtest -Djtest.config="builtin://Unit Tests"


=================================================

����Ӱ�����

Maven �� Gradle ֧�ֲ���Ӱ�������

Windows:

1. ʹ�� Maven �� Gradle ���в��ԣ����ռ����ڲ��Ժ͸����ʵĻ�������:
   mvnw clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=tia
   ��
   gradlew clean jtest-agent test jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=tia

   ע��: ��ˣ�report.xml �� cover .xml �ļ����� 'tia' ���ļ����д����� 

2. �޸Ĳ��Է�Χ�е�Դ�ļ�:
   src\main\java\examples\mock\FileExample.java

3. ��������������ִ���ܸ���Ӱ��Ĳ���:
   mvnw clean tia:affected-tests test -Djtest.referenceCoverageFile=tia/coverage.xml -Djtest.referenceReportFile=tia/report.xml
   ��
   gradlew clean affectedTests test -Djtest.referenceCoverageFile=tia/coverage.xml -Djtest.referenceReportFile=tia/report.xml

   ���ܴ����޸�Ӱ��Ĳ��Բ���ִ�С�

UNIX:

1. ʹ�� Maven �� Gradle ���в��ԣ����ռ����Ժ͸����ʵĻ�������:
   ./mvnw clean test-compile jtest:agent test jtest:jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=tia
   ��
   ./gradlew clean jtest-agent test jtest -Djtest.config="builtin://Unit Tests" -Djtest.report=tia

   ע��: ��ˣ�report.xml �� coverage.xml �ļ����� 'tia' ���ļ����д�����

2. �޸Ĳ��Է�Χ�е�Դ�ļ�:
   src/main/java/examples/mock/FileExample.java

3. ��������������ִ���ܸ���Ӱ��Ĳ���:
   ./mvnw clean tia:affected-tests test -Djtest.referenceCoverageFile=tia/coverage.xml -Djtest.referenceReportFile=tia/report.xml
   ��
   ./gradlew clean affectedTests test -Djtest.referenceCoverageFile=tia/coverage.xml -Djtest.referenceReportFile=tia/report.xml

   ���ܴ����޸�Ӱ��Ĳ��Բ���ִ�С�


�йظ������飬�����:
   https://docs.parasoft.com/display/JTEST20242/Testing+and+Analysis+with+Maven
   https://docs.parasoft.com/display/JTEST20242/Testing+and+Analysis+with+Gradle

=================================================

�ռ�Ӧ�ó��򸲸���

Windows:

1. ����Ӧ�ó����ռ�������������
     ant -file jtest.xml clean jtest-monitor
     ��
     mvnw clean package jtest:monitor    
     ��
     gradlew clean assemble jtest-monitor
     
   ע��: ��ˣ���Ӧ�û�� monitor.zip �ļ���

2. ����Ӧ�ó����ռ�����������
     
   a) �� monitor.zip �鵵�ļ���ѹ�� "demo" Ŀ¼�У���������Ŀ¼ "monitor"����
      ant:
        Archive path: parasoft\jtest-monitor\monitor.zip
      mvn:
        Archive path: target\jtest\monitor\monitor.zip
      gradle:
        Archive path: build\jtest\monitor.zip
     
   b) ���� agent.bat
      cd monitor
      agent.bat
      cd ..
      
   c) ʹ�� b) �����ɵ� Java VM ��������Ӧ�ó���
      ant
        java -cp demo.jar [ճ���� b �����ɵĲ���] examples.stackmachine.RunnableStackMachine
      mvn:
        java -cp target\Demo.jar [ճ���� b �����ɵĲ���] examples.stackmachine.RunnableStackMachine
      gradle:
        java -cp build\libs\demo.jar [ճ���� b �����ɵĲ���] examples.stackmachine.RunnableStackMachine

   d) ʹ�� "Stack Machine Example" Ӧ�ó���ִ�ж������:
      - ������ 123 ���뵽 "Input" �ֶ���
      - ��ѹ "push" ��ť 5 ��
      - ��ѹ "+", "-", "x" �� "/" ��ť
      - �˳�Ӧ�ó���

3. ���ɸ����ʱ���

     ..\..\jtestcli.exe -config "builtin://Calculate Application Coverage" -staticcoverage monitor\static_coverage.xml -runtimecoverage monitor\runtime_coverage

     �����ʵ���ϸ��Ϣ������ report.html ���ҵ�

UNIX:

1. ����Ӧ�ó����ռ��������������
     ant -file jtest.xml clean jtest-monitor
     ��
     ./mvnw clean package jtest:monitor    
     ��
     ./gradlew clean build jtest-monitor
     
   ע��: ��ˣ���Ӧ�û�� monitor.zip �ļ���

2. ����Ӧ�ó����ռ�����������
   
   a) �� monitor.zip �鵵�ļ���ѹ�� demo ·���ϣ���������Ŀ¼���ӣ�
      ant:
        unzip ./parasoft/jtest-monitor/monitor.zip
      mvn: 
        unzip ./target/jtest/monitor/monitor.zip
      gradle:
        unzip ./build/jtest/monitor.zip
     
   b) ���� agent.sh
      ./monitor/agent.sh
      
   c) ʹ�� b) �����ɵ� Java VM ��������Ӧ�ó���
      ant
        java -cp ./demo.jar [ճ���� b �����ɵĲ���] examples.stackmachine.RunnableStackMachine
      mvn:
        java -cp ./target/Demo.jar [ճ���� b �����ɵĲ���] examples.stackmachine.RunnableStackMachine
      gradle:
        java -cp ./build/libs/demo.jar [ճ���� b �����ɵĲ���] examples.stackmachine.RunnableStackMachine

   d) ʹ�� "Stack Machine Example" Ӧ�ó���ִ���������
      - ������ 123 ���뵽 "Input" �ֶ���
      - ��ѹ "push" ��ť 5 ��
      - ��ѹ "+", "-", "x" �� "/" ��ť
      - �˳�Ӧ�ó���

3. ���ɸ����ʱ���

     ../../jtestcli -config "builtin://Calculate Application Coverage" -staticcoverage ./monitor/static_coverage.xml -runtimecoverage ./monitor/runtime_coverage

     �����ʵ���ϸ��Ϣ������ report.html ���ҵ�


�йظ������飬����� https://docs.parasoft.com/display/JTEST20242/Application+Coverage
