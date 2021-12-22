pipeline {
  agent any
  stages {
    stage('Check') {
      steps {
        sh '''sed -e "s/\\./\\n/g" production/trust-list-production | split -l 1
trust_list_count=$(base64 -d xab | jq | egrep "   \\"..\\": {" | wc -l)
if [[ $trust_list_count -gt 48 ]]
then
  cp trust-list-production-$date /storage/eudcc-data/production
  cp trust-list-production-$date /storage/eudcc-data/production/trust-list
  base64 -d xab | jq | mailx -v -s "[INFO] trust-list production: $trust_list_count countries" -S smtp-use-starttls -S smtp-auth=login -S smtp=smtp://smtp.gmail.com:587 -S from="fabricio.tamusiunas@gmail.com" -S smtp-auth-user="fabricio.tamusiunas@gmail.com" -S smtp-auth-password="ahfdjzplegzpdjhi" fabricio.tamusiunas@gmail.com
else
  base64 -d xab | jq | mailx -v -s "[ERROR] trust-list production: $trust_list_count countries" -S smtp-use-starttls -S smtp-auth=login -S smtp=smtp://smtp.gmail.com:587 -S from="fabricio.tamusiunas@gmail.com" -S smtp-auth-user="fabricio.tamusiunas@gmail.com" -S smtp-auth-password="ahfdjzplegzpdjhi" fabricio.tamusiunas@gmail.com
fi
'''
      }
    }

  }
}