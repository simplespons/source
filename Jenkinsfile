pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'echo  Building'
            }
        }
        stage('Test') { 
            steps {
                sh ' echo Hello'
            }
        }


        stage('Deploy to stageing') { 
            steps {
                sh 'ssh -o StrictHostKeyChecking=no root@85.31.233.43 "source venv/bin/activate; \
                cd 1.todo; \
                git pull origin master; \
                pip install -r requerment.txt --no-warn-script-location; \
                python3 manage.py collectstatic; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restart gunicorn"'
                   }
                }

        stage('Deploy to prod') { 
   
               input { 

                message "shell you deploy to producttion"
                ok  "yes"
            }
         
            steps {
                sh 'ssh -o StrictHostKeyChecking=no root@85.31.233.43 "source venv/bin/activate; \
                cd 1.todo; \
                git pull origin master; \
                pip install -r requerment.txt --no-warn-script-location; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restart gunicorn"'



            }
        }
    }
}
