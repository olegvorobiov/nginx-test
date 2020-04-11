pipeline {
    agent {
        label "wombat"
    } // agent
    stages {
        stage("Create docker image for testing") {
            sh """
                python3 -m molecule create
            """
        } // stage
        stage("Apply ansible role to docker image") {
            steps {
                sh """
                    python3 -m molecule converge
                """
            } // steps
        } // stage
        stage("Check idempotency") {
            steps {
                sh """
                    python3 -m molecule idempotence
                """
            } // steps
        } // stage
        stage("Cleanup molecule") {
            steps {
                sh """
                    python3 -m molecule cleanup
                """
            } // steps
        } // stage
        stage("Destroy molecule instance") {
            steps {
                sh """
                    python3 -m molecule destroy
                """
            } // steps
        } // stage
    } // stages
} // pipeline