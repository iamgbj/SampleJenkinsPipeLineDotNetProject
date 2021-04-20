pipeline {
    agent any

    stages {
        stage('Create Local Folder') {
            steps {
                bat '''if not exist "F:\\JenkinsCopy\\DotNetSampleWebApp" mkdir F:\\JenkinsCopy\\DotNetSampleWebApp &
				xcopy /s .\\DotNetSampleWebApp F:\\JenkinsCopy\\DotNetSampleWebApp'''
            }
        }
		stage('Restore Nuget Packages') {
            steps {
                bat '"C:\\tools\\NuGet.exe" restore F:\\JenkinsCopy\\DotNetSampleWebApp\\'
            }
        }
		stage('Build') {
            steps {
                bat "\"${tool 'MSBuild'}\" F:\JenkinsCopy\DotNetSampleWebApp\DotNetSampleWebApp.sln /p:Configuration=Debug /p:Platform=\"Any CPU\" /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
            }
        }
		stage('Archive') {
            steps {
                bat '@RD /S /Q "F:\\JenkinsCopy\\DotNetSampleWebApp"'
            }
        }
    }
}