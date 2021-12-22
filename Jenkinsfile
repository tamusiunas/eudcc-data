pipeline {
  agent any
  stages {
    stage('Check') {
      steps {
        sh '''sed -e "s/\\./\\n/g" production/trust-list | split -l 1
ls -l
trust_list_count=$(base64 -d xab | jq | egrep \\"   \\\\\\"..\\\\\\": {\\" )
if [[ $trust_list_count -gt 48 ]]
then
# base64 -d xab | jq | mailx -v -s "[INFO] trust-list production: $trust_list_count countries" -S smtp-use-starttls -S smtp-auth=login -S smtp=smtp://smtp.gmail.com:587 -S from="fabricio.tamusiunas@gmail.com" -S smtp-auth-user="fabricio.tamusiunas@gmail.com" -S smtp-auth-password="ahfdjzplegzpdjhi" fabricio.tamusiunas@gmail.com
  echo "OK"
else
# base64 -d xab | jq | mailx -v -s "[ERROR] trust-list production: $trust_list_count countries" -S smtp-use-starttls -S smtp-auth=login -S smtp=smtp://smtp.gmail.com:587 -S from="fabricio.tamusiunas@gmail.com" -S smtp-auth-user="fabricio.tamusiunas@gmail.com" -S smtp-auth-password="ahfdjzplegzpdjhi" fabricio.tamusiunas@gmail.com
  echo "ERROR"
fi
'''
      }
    }

  }
}