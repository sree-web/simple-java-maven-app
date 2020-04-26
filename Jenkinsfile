pipeline{
     
     tools{
          jdk 'Default'
          maven 'maven'
     }
         
     agent none
     stages{
         stage('Checkout'){
             agent any
             steps{
                 git 'https://github.com/sree-web/simple-java-maven-app.git'
             }
         }
          stage('Project-compile'){
              agent any
              steps{
                  sh 'mvn compile'
              }
         } 
          stage('Project-code review'){
              agent any
              steps{
                  sh 'mvn pmd:pmd'
              }
              post{
                    always{
                        pmd pattern: 'target/pmd.xml'
                    }
                    
              }
          
          }
           stage('Project Unit test'){
               agent any
               steps{
                   sh 'mvn test'
                
               }
               post{
                   always{
                       junit 'target/surefire-reports/*.xml'
                   }
               }
               
          }    
           stage('Project-Matrixcheck'){
               agent {label 'windows'}
               steps{
                   git 'https://github.com/sree-web/simple-java-maven-app.git'
                   bat 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                   
 
               }
               post{
                   always{
                       cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                   }
               }
           } 
            stage('Project-packaging'){
                agent {label 'windows'}
                steps{
                    bat 'mvn package'
                }
            }
     }
 }

