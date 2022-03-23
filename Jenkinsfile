// Declarativa: Es más cómoda... más guiada... menos flexible
pipeline {
    // Integración continua
    agent any;
    // Parametros
    parameters {
        booleanParam description: 'Quiere hacer pruebas de HA?', name: 'PROBAR_HA'
        choice choices: ['chrome', 'firefox'], description: 'Qué navegador usar para las pruebas de UI básicas', name: 'NAVEGADOR_PRUEBAS_BASICAS'
    }

    stages {
        stage('1-Compilación') {
            steps {
                echo 'Voy a compilar:'
                echo 'Estoy en ello.....'
                echo 'Listo'
            }
            post {
                success {
                    echo 'Se ejecuta solo si los steps han ido bien'
                }
                failure {
                    echo 'Se ejecuta solo si los steps han ido mal'
                }
                always {
                    echo 'Se ejecuta en cualquier caso'
                }
            }
        }    
        stage('2-Pruebas Nivel I') {
            
            stages {
                stage('2.1-Pruebas Unitarias') {
                    steps {
                        echo 'Pruebas unitarias'
                    }
                    //post
                    post {
                        always {
                            echo 'Publicar el informe de las pruebas'
                        }
                    }
                }
                stage('2.2-Pruebas De Calidad') {
                    steps {
                        echo 'Llamar sonarqube'
                    }
                    //post
                }
            }
            
        }    
        // Despliegue + Pruebas
        //stage('2,5-Creación de un entorno de integración') {}
        stage('3-Instalación en entorno de integración') {
            stages{
                stage('3.1-Despliegue') {
                    steps {
                        echo 'Instalación de app'
                    }
                }    
                stage('3.2-Smoketest') {
                    steps {
                        echo 'Probar si la app se ha instalado bien'
                    }
                }    
            }
        }
        stage('5-Más Pruebas') {
            parallel {
                stage('5.1-Resto de pruebas funcionales') {
                    steps {
                        echo 'Pruebas de integración, sistema, aceptación... 15 minutos'
                    }
                }    
                stage('5.2-UI Básicas') {
                    steps {
                        echo "Pruebas selenium en $params.NAVEGADOR_PRUEBAS_BASICAS - $NAVEGADOR_PRUEBAS_BASICAS y en ultima versión... 30 minutos"
                    }
                }
            }
        }
        stage('6-Pruebas especiales') {
            stages {
                stage('6.1-Rendimiento') {
                    steps {
                        echo 'Jmeter, Loadrunner 1 -> Linea base'
                        echo 'Jmeter, Loadrunner media carga'
                        echo 'Jmeter, Loadrunner carga completa'
                        echo 'Jmeter, Loadrunner doble carga'
                    }
                }    
                stage('6.2-HA') {
                    steps {
                        echo 'Probar alta disponibilidad'
                    }
                    when {
                        expression {
                            return params.PROBAR_HA == 'true';
                        }
                    }
                }    
                stage('6.3-UI Completas') {
                    stages{
                        // Selenium-Grid
                        stage('6.3.1-Chrome') {
                            steps {
                                echo 'Android telefono'
                                echo 'Android tableta'
                                echo 'Windows7'
                                echo 'Windows8'
                                echo 'Windows10'
                                echo 'Windows11'
                                echo 'MacOS'
                                echo 'Ubuntu'
                                echo 'Fedora'
                            }
                        }    
                        stage('6.3.2-Firefox') {
                            steps {
                                echo 'Windows7'
                                echo 'Windows8'
                                echo 'Windows10'
                                echo 'Windows11'
                                echo 'MacOS'
                                echo 'Ubuntu'
                                echo 'Fedora'
                            }
                        }    
                        stage('6.3.3-Safari') {
                            steps {
                                echo 'MacOS'
                                echo 'iOS'
                            }
                        }    
                        stage('6.3.4-Edge') {
                            steps {
                                echo 'Windows7'
                                echo 'Windows8'
                                echo 'Windows10'
                                echo 'Windows11'
                            }                       
                        }    
                        stage('6.3.5-Opera') {
                            steps {
                                echo 'Windows7'
                                echo 'Windows8'
                                echo 'Windows10'
                                echo 'Windows11'
                                echo 'MacOS'
                                echo 'Ubuntu'
                                echo 'Fedora'
                            }                        
                        }    
                    }
                }    
            }
        }
        // Aqui estamos en el limite de lo que es Entrega continua
        stage('7-Guardo el artefacto') {
            step {
                echo 'En un repo de artefactos: NEXUS, ARTIFACTORY, REGISTRY DE IMAGENES DE DOCKER'
            }
        }
    }
    
    // Tanto la marca post, como las marcas de dentro son opcionales
    post {
        always {
            echo 'Limpieza de la basura que se haya generado entre medias'
        }
    }

}

// Scripted: Es más potente, más flexible.... menos cómoda. LA BUENA !!