TWO Ways to do a Deploy Continuos: 

1 - This script can be used with Puppet Dashboard, create a module and put these lines in manifests for control de version of APP by Dashboard Puppet Enterprise.

File: init.pp
if $app_version {     notify {"Versao do APP: ${app_version}":}     
	exec {"atualizando_deploy_app_version":       
	path    => "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin",      
	command => "puppet-nexus.sh -a \"br.com.app:nameapp:${app_version}\" -e 'war' -n 'http://servernexus.domain:8081/nexus' -r 'releases' -o '/etc/puppetlabs/puppet/environments/production/modules/jboss/files/deploys_producao/app.war'",
 	}
   }
   
   
2 - Another way is execute the script by Jenkins Application for development environments when finish deploy and publish in Nexus Server create a new JOB to execute Puppet-Deploy to lastest version App deploy. And put the feature SSH Command: 

Confs Jenkins Job:
User: puppet-deploy
puppet-nexus.sh -a "br.com.app:appname:LATEST" -e 'war' -n 'http://dev-nexus.cianot.com.br:8081/nexus' -r 'snapshots' -o '/etc/puppetlabs/puppet/environments/development/modules/jboss/files/deploys_producao''environment puppet' 'dev-jboss-server.domain'
   
   NOTE: Put the script "puppet-nexus" in Puppet Server, directory recommended: "/usr/loca/bin/"
