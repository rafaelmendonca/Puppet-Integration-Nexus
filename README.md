This script can be used with Puppet Dashboard, create a module and put these lines in manifests.

File: init.pp
if $app_version {     notify {"Versao do APP: ${app_version}":}     
	exec {"atualizando_deploy_app_version":       
	path    => "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin",      
	 command => "puppet-nexus.sh -a \"br.com.app:nameapp:${app_version}\" -e 'war' -n 'http://servernexus.domain:8081/nexus' -r 'releases' -o '/etc/puppetlabs/puppet/environments/production/modules/jboss/files/deploys_producao/app.war'",
	     }
   }