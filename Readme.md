## First add bitnami because we will use bitnami rabbitmq helm cahrt

helm repo add bitnami https://charts.bitnami.com/bitnami
helm install rabbitmq bitnami/rabbitmq -f rabbitmq-custom-valuse.yaml
```
Here in custom values i just made few chenge like set root user name as 
and password as admin


here below i provide my custom values

```yaml
## @section Global parameters
## Global Docker image parameters
## Please, note that this will override the image parameters, including dependencies, configured to use the global value
## Current available global Docker image parameters: imageRegistry, imagePullSecrets and storageClass
##

## @param global.imageRegistry Global Docker image registry
## @param global.imagePullSecrets Global Docker registry secret names as an array
## @param global.storageClass Global StorageClass for Persistent Volume(s)
##
global:
  imageRegistry: ""
  ## E.g.
  ## imagePullSecrets:
  ##   - myRegistryKeySecretName
  ##
  imagePullSecrets: []
  storageClass: ""

## @section RabbitMQ Image parameters
## Bitnami RabbitMQ image version
## ref: https://hub.docker.com/r/bitnami/rabbitmq/tags/
## @param image.registry RabbitMQ image registry
## @param image.repository RabbitMQ image repository
## @param image.tag RabbitMQ image tag (immutable tags are recommended)
## @param image.digest RabbitMQ image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag
## @param image.pullPolicy RabbitMQ image pull policy
## @param image.pullSecrets Specify docker-registry secret names as an array
## @param image.debug Set to true if you would like to see extra information on logs
##
image:
  registry: docker.io
  repository: bitnami/rabbitmq
  tag: 3.10.8-debian-11-r4
  digest: ""
  ## set to true if you would like to see extra information on logs
  ## It turns BASH and/or NAMI debugging in the image
  ##
  debug: false
  ## Specify a imagePullPolicy
  ## Defaults to 'Always' if image tag is 'latest', else set to 'IfNotPresent'
  ## ref: https://kubernetes.io/docs/user-guide/images/#pre-pulling-images
  ##
  pullPolicy: IfNotPresent
  ## Optionally specify an array of imagePullSecrets.
  ## Secrets must be manually created in the namespace.
  ## ref: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
  ## Example:
  ## pullSecrets:
  ##   - myRegistryKeySecretName
  ##
  pullSecrets: []

## @section Common parameters
##

## @param nameOverride String to partially override rabbitmq.fullname template (will maintain the release name)
##
nameOverride: ""
## @param fullnameOverride String to fully override rabbitmq.fullname template
##
fullnameOverride: ""
## @param namespaceOverride String to fully override common.names.namespace
##
namespaceOverride: ""
## @param kubeVersion Force target Kubernetes version (using Helm capabilities if not set)
##
kubeVersion: ""
## @param clusterDomain Kubernetes Cluster Domain
##
clusterDomain: cluster.local
## @param extraDeploy Array of extra objects to deploy with the release
##
extraDeploy: []
## @param commonAnnotations Annotations to add to all deployed objects
##
commonAnnotations: {}
## @param commonLabels Labels to add to all deployed objects
##
commonLabels: {}
## Enable diagnostic mode in the deployment
##
diagnosticMode:
  ## @param diagnosticMode.enabled Enable diagnostic mode (all probes will be disabled and the command will be overridden)
  ##
  enabled: false
  ## @param diagnosticMode.command Command to override all containers in the deployment
  ##
  command:
    - sleep
  ## @param diagnosticMode.args Args to override all containers in the deployment
  ##
  args:
    - infinity

## @param hostAliases Deployment pod host aliases
## https://kubernetes.io/docs/concepts/services-networking/add-entries-to-pod-etc-hosts-with-host-aliases/
##
hostAliases: []
## @param dnsPolicy DNS Policy for pod
## ref: https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/
## E.g.
## dnsPolicy: ClusterFirst
##
dnsPolicy: ""
## @param dnsConfig DNS Configuration pod
## ref: https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/
## E.g.
## dnsConfig:
##   options:
##   - name: ndots
##     value: "4"
##
dnsConfig: {}
## RabbitMQ Authentication parameters
##
auth:
  ## @param auth.username RabbitMQ application username
  ## ref: https://github.com/bitnami/containers/tree/main/bitnami/rabbitmq#environment-variables
  ##
  username: admin
  ## @param auth.password RabbitMQ application password
  ## ref: https://github.com/bitnami/containers/tree/main/bitnami/rabbitmq#environment-variables
  ##
  password: "admin"
  ## @param auth.existingPasswordSecret Existing secret with RabbitMQ credentials (must contain a value for `rabbitmq-password` key)
  ## e.g:
  ## existingPasswordSecret: name-of-existing-secret
  ##
  existingPasswordSecret: ""
  ## @param auth.erlangCookie Erlang cookie to determine whether different nodes are allowed to communicate with each other
  ## ref: https://github.com/bitnami/containers/tree/main/bitnami/rabbitmq#environment-variables
  ##
  erlangCookie: ""
  ## @param auth.existingErlangSecret Existing secret with RabbitMQ Erlang cookie (must contain a value for `rabbitmq-erlang-cookie` key)
  ## e.g:
  ## existingErlangSecret: name-of-existing-secret
  ##
  existingErlangSecret: ""

  ## Enable encryption to rabbitmq
  ## ref: https://www.rabbitmq.com/ssl.html
  ## @param auth.tls.enabled Enable TLS support on RabbitMQ
  ## @param auth.tls.autoGenerated Generate automatically self-signed TLS certificates
  ## @param auth.tls.failIfNoPeerCert When set to true, TLS connection will be rejected if client fails to provide a certificate
  ## @param auth.tls.sslOptionsVerify Should [peer verification](https://www.rabbitmq.com/ssl.html#peer-verification) be enabled?
  ## @param auth.tls.caCertificate Certificate Authority (CA) bundle content
  ## @param auth.tls.serverCertificate Server certificate content
  ## @param auth.tls.serverKey Server private key content
  ## @param auth.tls.existingSecret Existing secret with certificate content to RabbitMQ credentials
  ## @param auth.tls.existingSecretFullChain Whether or not the existing secret contains the full chain in the certificate (`tls.crt`). Will be used in place of `ca.cert` if `true`.
  ##
  tls:
    enabled: false
    autoGenerated: false
    failIfNoPeerCert: true
    sslOptionsVerify: verify_peer
    caCertificate: |-
    serverCertificate: |-
    serverKey: |-
    existingSecret: ""
    existingSecretFullChain: false

## @param logs Path of the RabbitMQ server's Erlang log file. Value for the `RABBITMQ_LOGS` environment variable
## ref: https://www.rabbitmq.com/logging.html#log-file-location
##
logs: "-"
## @param ulimitNofiles RabbitMQ Max File Descriptors
## ref: https://github.com/bitnami/containers/tree/main/bitnami/rabbitmq#environment-variables
## ref: https://www.rabbitmq.com/install-debian.html#kernel-resource-limits
##
ulimitNofiles: "65536"
## RabbitMQ maximum available scheduler threads and online scheduler threads. By default it will create a thread per CPU detected, with the following parameters you can tune it manually.
## ref: https://hamidreza-s.github.io/erlang/scheduling/real-time/preemptive/migration/2016/02/09/erlang-scheduler-details.html#scheduler-threads
## ref: https://github.com/bitnami/charts/issues/2189
## @param maxAvailableSchedulers RabbitMQ maximum available scheduler threads
## @param onlineSchedulers RabbitMQ online scheduler threads
##
maxAvailableSchedulers: ""
onlineSchedulers: ""

## The memory threshold under which RabbitMQ will stop reading from client network sockets, in order to avoid being killed by the OS
## ref: https://www.rabbitmq.com/alarms.html
## ref: https://www.rabbitmq.com/memory.html#threshold
##
memoryHighWatermark:
  ## @param memoryHighWatermark.enabled Enable configuring Memory high watermark on RabbitMQ
  ##
  enabled: false
  ## @param memoryHighWatermark.type Memory high watermark type. Either `absolute` or `relative`
  ##
  type: "relative"
  ## Memory high watermark value.
  ## @param memoryHighWatermark.value Memory high watermark value
  ## The default value of 0.4 stands for 40% of available RAM
  ## Note: the memory relative limit is applied to the resource.limits.memory to calculate the memory threshold
  ## You can also use an absolute value, e.g.: 256MB
  ##
  value: 0.4

## @param plugins List of default plugins to enable (should only be altered to remove defaults; for additional plugins use `extraPlugins`)
##
plugins: "rabbitmq_management rabbitmq_peer_discovery_k8s"
## @param communityPlugins List of Community plugins (URLs) to be downloaded during container initialization
## Combine it with extraPlugins to also enable them.
##
communityPlugins: ""
## @param extraPlugins Extra plugins to enable (single string containing a space-separated list)
## Use this instead of `plugins` to add new plugins
##
extraPlugins: "rabbitmq_auth_backend_ldap"

## Clustering settings
##
clustering:
  ## @param clustering.enabled Enable RabbitMQ clustering
  ##
  enabled: true
  ## @param clustering.addressType Switch clustering mode. Either `ip` or `hostname`
  ##
  addressType: hostname
  ## @param clustering.rebalance Rebalance master for queues in cluster when new replica is created
  ## ref: https://www.rabbitmq.com/rabbitmq-queues.8.html#rebalance
  ##
  rebalance: false
  ## @param clustering.forceBoot Force boot of an unexpectedly shut down cluster (in an unexpected order).
  ## forceBoot executes 'rabbitmqctl force_boot' to force boot cluster shut down unexpectedly in an unknown order
  ## ref: https://www.rabbitmq.com/rabbitmqctl.8.html#force_boot
  ##
  forceBoot: false
  ## @param clustering.partitionHandling Switch Partition Handling Strategy. Either `autoheal` or `pause-minority` or `pause-if-all-down` or `ignore`
  ## ref: https://www.rabbitmq.com/partitions.html#automatic-handling
  ##
  partitionHandling: autoheal

## Loading a RabbitMQ definitions file to configure RabbitMQ
##
loadDefinition:
  ## @param loadDefinition.enabled Enable loading a RabbitMQ definitions file to configure RabbitMQ
  ##
  enabled: false
  ## @param loadDefinition.file Name of the definitions file
  ##
  file: "/app/load_definition.json"
  ## @param loadDefinition.existingSecret Existing secret with the load definitions file
  ## Can be templated if needed, e.g:
  ## existingSecret: "{{ .Release.Name }}-load-definition"
  ##
  existingSecret: ""

## @param command Override default container command (useful when using custom images)
##
command: []
## @param args Override default container args (useful when using custom images)
##
args: []
## @param lifecycleHooks Overwrite livecycle for the RabbitMQ container(s) to automate configuration before or after startup
##
lifecycleHooks: {}
## @param terminationGracePeriodSeconds Default duration in seconds k8s waits for container to exit before sending kill signal.
## Any time in excess of 10 seconds will be spent waiting for any synchronization necessary for cluster not to lose data.
##
terminationGracePeriodSeconds: 120
## @param extraEnvVars Extra environment variables to add to RabbitMQ pods
## E.g:
## extraEnvVars:
##   - name: FOO
##     value: BAR
##
extraEnvVars: []
## @param extraEnvVarsCM Name of existing ConfigMap containing extra environment variables
##
extraEnvVarsCM: ""
## @param extraEnvVarsSecret Name of existing Secret containing extra environment variables (in case of sensitive data)
##
extraEnvVarsSecret: ""

## Container Ports
## @param containerPorts.amqp
## @param containerPorts.amqpTls
## @param containerPorts.dist
## @param containerPorts.manager
## @param containerPorts.epmd
## @param containerPorts.metrics
##
containerPorts:
  amqp: 5672
  amqpTls: 5671
  dist: 25672
  manager: 15672
  epmd: 4369
  metrics: 9419

## @param initScripts Dictionary of init scripts. Evaluated as a template.
## Specify dictionary of scripts to be run at first boot
## Alternatively, you can put your scripts under the files/docker-entrypoint-initdb.d directory
## For example:
## initScripts:
##   my_init_script.sh: |
##      #!/bin/sh
##      echo "Do something."
##
initScripts: {}
## @param initScriptsCM ConfigMap with the init scripts. Evaluated as a template.
## Note: This will override initScripts
##
initScriptsCM: ""
## @param initScriptsSecret Secret containing `/docker-entrypoint-initdb.d` scripts to be executed at initialization time that contain sensitive data. Evaluated as a template.
##
initScriptsSecret: ""
## @param extraContainerPorts Extra ports to be included in container spec, primarily informational
## E.g:
## extraContainerPorts:
## - name: new_port_name
##   containerPort: 1234
##
extraContainerPorts: []
## @param configuration [string] RabbitMQ Configuration file content: required cluster configuration
## Do not override unless you know what you are doing.
## To add more configuration, use `extraConfiguration` of `advancedConfiguration` instead
##
configuration: |-
  ## Username and password
  ##
  default_user = {{ .Values.auth.username }}
  default_pass = CHANGEME
  {{- if .Values.clustering.enabled }}
  ## Clustering
  ##
  cluster_formation.peer_discovery_backend  = rabbit_peer_discovery_k8s
  cluster_formation.k8s.host = kubernetes.default
  cluster_formation.node_cleanup.interval = 10
  cluster_formation.node_cleanup.only_log_warning = true
  cluster_partition_handling = {{ .Values.clustering.partitionHandling }}
  {{- end }}
  {{- if .Values.loadDefinition.enabled }}
  load_definitions = {{ .Values.loadDefinition.file }}
  {{- end }}
  # queue master locator
  queue_master_locator = min-masters
  # enable guest user
  loopback_users.guest = false
  {{ tpl .Values.extraConfiguration . }}
  {{- if .Values.auth.tls.enabled }}
  ssl_options.verify = {{ .Values.auth.tls.sslOptionsVerify }}
  listeners.ssl.default = {{ .Values.service.ports.amqpTls }}
  ssl_options.fail_if_no_peer_cert = {{ .Values.auth.tls.failIfNoPeerCert }}
  ssl_options.cacertfile = /opt/bitnami/rabbitmq/certs/ca_certificate.pem
  ssl_options.certfile = /opt/bitnami/rabbitmq/certs/server_certificate.pem
  ssl_options.keyfile = /opt/bitnami/rabbitmq/certs/server_key.pem
  {{- end }}
  {{- if .Values.ldap.enabled }}
  auth_backends.1.authn = ldap
  auth_backends.1.authz = {{ ternary "ldap" "internal" .Values.ldap.authorisationEnabled }}
  auth_backends.2 = internal
  {{- $host :=  list }}
  {{- $port :=  ternary 636 389 .Values.ldap.tls.enabled }}
  {{- if .Values.ldap.uri }}
  {{- $hostPort := get (urlParse .Values.ldap.uri) "host" }}
  {{- $host = list (index (splitList ":" $hostPort) 0) -}}
  {{- if (contains ":" $hostPort) }}
  {{- $port = index (splitList ":" $hostPort) 1 -}}
  {{- end }}
  {{- end }}
  {{- range $index, $server := concat $host .Values.ldap.servers }}
  auth_ldap.servers.{{ add $index 1 }} = {{ $server }}
  {{- end }}
  auth_ldap.port = {{ coalesce .Values.ldap.port $port }}
  {{- if or .Values.ldap.user_dn_pattern .Values.ldap.userDnPattern }}
  auth_ldap.user_dn_pattern = {{ coalesce .Values.ldap.user_dn_pattern .Values.ldap.userDnPattern }}
  {{- end }}
  {{- if .Values.ldap.basedn }}
  auth_ldap.dn_lookup_base = {{ .Values.ldap.basedn }}
  {{- end }}
  {{- if .Values.ldap.uidField }}
  auth_ldap.dn_lookup_attribute = {{ .Values.ldap.uidField }}
  {{- end }}
  {{- if .Values.ldap.binddn }}
  auth_ldap.dn_lookup_bind.user_dn = {{ .Values.ldap.binddn }}
  auth_ldap.dn_lookup_bind.password = {{ required "'ldap.bindpw' is required when 'ldap.binddn' is defined" .Values.ldap.bindpw }}
  {{- end }}
  {{- if .Values.ldap.tls.enabled }}
  auth_ldap.use_ssl = {{ not .Values.ldap.tls.startTls }}
  auth_ldap.use_starttls = {{ .Values.ldap.tls.startTls }}
  {{- if .Values.ldap.tls.CAFilename }}
  auth_ldap.ssl_options.cacertfile = {{ .Values.ldap.tls.certificatesMountPath }}/{{ .Values.ldap.tls.CAFilename }}
  {{- end }}
  {{- if .Values.ldap.tls.certFilename }}
  auth_ldap.ssl_options.certfile = {{ .Values.ldap.tls.certificatesMountPath }}/{{ .Values.ldap.tls.certFilename }}
  auth_ldap.ssl_options.keyfile = {{ .Values.ldap.tls.certificatesMountPath }}/{{ required "'ldap.tls.certKeyFilename' is required when 'ldap.tls.certFilename' is defined" .Values.ldap.tls.certKeyFilename }}
  {{- end }}
  {{- if .Values.ldap.tls.skipVerify }}
  auth_ldap.ssl_options.verify = verify_none
  auth_ldap.ssl_options.fail_if_no_peer_cert = false
  {{- else if .Values.ldap.tls.verify }}
  auth_ldap.ssl_options.verify = {{ .Values.ldap.tls.verify }}
  {{- end }}
  {{- end }}
  {{- end }}
  {{- if .Values.metrics.enabled }}
  ## Prometheus metrics
  ##
  prometheus.tcp.port = 9419
  {{- end }}
  {{- if .Values.memoryHighWatermark.enabled }}
  ## Memory Threshold
  ##
  total_memory_available_override_value = {{ include "rabbitmq.toBytes" .Values.resources.limits.memory }}
  vm_memory_high_watermark.{{ .Values.memoryHighWatermark.type }} = {{ .Values.memoryHighWatermark.value }}
  {{- end }}

## @param extraConfiguration [string] Configuration file content: extra configuration to be appended to RabbitMQ configuration
## Use this instead of `configuration` to add more configuration
##
extraConfiguration: |-
  #default_vhost = {{ .Release.Namespace }}-vhost
  #disk_free_limit.absolute = 50MB

## @param advancedConfiguration Configuration file content: advanced configuration
## Use this as additional configuration in classic config format (Erlang term configuration format)
##
## LDAP authorisation example:
## advancedConfiguration: |-
##   [{rabbitmq_auth_backend_ldap,[
##      {tag_queries,           [{administrator, {constant, true}},
##                               {management,    {constant, true}}]}
##   ]}].
##
advancedConfiguration: |-

## LDAP configuration
##
ldap:
  ## @param ldap.enabled Enable LDAP support
  ##
  enabled: false
  ## @param ldap.uri LDAP connection string.
  ##
  uri: ""
  ## @param ldap.servers List of LDAP servers hostnames. This is valid only if ldap.uri is not set
  ##
  servers: []
  ## @param ldap.port LDAP servers port. This is valid only if ldap.uri is not set
  ##
  port: ""

  ## DEPRECATED ldap.user_dn_pattern it will removed in a future, please use userDnPattern instead
  ## Pattern used to translate the provided username into a value to be used for the LDAP bind
  ## @param ldap.userDnPattern Pattern used to translate the provided username into a value to be used for the LDAP bind.
  ## ref: https://www.rabbitmq.com/ldap.html#usernames-and-dns
  ##
  userDnPattern: ""
  ## @param ldap.binddn DN of the account used to search in the LDAP server.
  ##
  binddn: ""
  ## @param ldap.bindpw Password for binddn account.
  ##
  bindpw: ""
  ## @param ldap.basedn Base DN path where binddn account will search for the users.
  ##
  basedn: ""
  ## @param ldap.uidField Field used to match with the user name (uid, samAccountName, cn, etc). It matches with 'dn_lookup_attribute' in RabbitMQ configuration
  ##��ref: https://www.rabbitmq.com/ldap.html#usernames-and-dns
  ##
  ## @param ldap.uidField Field used to match with the user name (uid, samAccountName, cn, etc). It matches with 'dn_lookup_attribute' in RabbitMQ configuration
  uidField: ""
  ## @param ldap.authorisationEnabled Enable LDAP authorisation. Please set 'advancedConfiguration' with tag, topic, resources and vhost mappings
  ## ref: https://www.rabbitmq.com/ldap.html#authorisation
  ##
  authorisationEnabled: false
  ## @param ldap.tls.enabled Enabled TLS configuration.
  ## @param ldap.tls.startTls Use STARTTLS instead of LDAPS.
  ## @param ldap.tls.skipVerify Skip any SSL verification (hostanames or certificates)
  ## @param ldap.tls.verify Verify connection. Valid values are 'verify_peer' or 'verify_none'
  ## @param ldap.tls.certificatesMountPath Where LDAP certifcates are mounted.
  ## @param ldap.tls.certificatesSecret Secret with LDAP certificates.
  ## @param ldap.tls.CAFilename  CA certificate filename. Should match with the CA entry key in the ldap.tls.certificatesSecret.
  ## @param ldap.tls.certFilename Client certificate filename to authenticate against the LDAP server. Should match with certificate the entry key in the ldap.tls.certificatesSecret.
  ## @param ldap.tls.certKeyFilename Client Key filename to authenticate against the LDAP server. Should match with certificate the entry key in the ldap.tls.certificatesSecret.
  ##
  tls:
    enabled: false
    startTls: false
    skipVerify: false
    verify: "verify_peer"
    certificatesMountPath: /opt/bitnami/rabbitmq/ldap/certs
    certificatesSecret: ""
    CAFilename: ""
    certFilename: ""
    certKeyFilename: ""

## @param extraVolumeMounts Optionally specify extra list of additional volumeMounts
## Examples:
## extraVolumeMounts:
##   - name: extras
##     mountPath: /usr/share/extras
##     readOnly: true
##
extraVolumeMounts: []
## @param extraVolumes Optionally specify extra list of additional volumes .
## Example:
## extraVolumes:
##   - name: extras
##     emptyDir: {}
##
extraVolumes: []
## @param extraSecrets Optionally specify extra secrets to be created by the chart.
## This can be useful when combined with load_definitions to automatically create the secret containing the definitions to be loaded.
## Example:
## extraSecrets:
##   load-definition:
##     load_definition.json: |
##       {
##         ...
##       }
##
extraSecrets: {}
## @param extraSecretsPrependReleaseName Set this flag to true if extraSecrets should be created with <release-name> prepended.
##
extraSecretsPrependReleaseName: false

## @section Statefulset parameters
##

## @param replicaCount Number of RabbitMQ replicas to deploy
##
replicaCount: 1
## @param schedulerName Use an alternate scheduler, e.g. "stork".
## ref: https://kubernetes.io/docs/tasks/administer-cluster/configure-multiple-schedulers/
##
schedulerName: ""
## RabbitMQ should be initialized one by one when building cluster for the first time.
## Therefore, the default value of podManagementPolicy is 'OrderedReady'
## Once the RabbitMQ participates in the cluster, it waits for a response from another
## RabbitMQ in the same cluster at reboot, except the last RabbitMQ of the same cluster.
## If the cluster exits gracefully, you do not need to change the podManagementPolicy
## because the first RabbitMQ of the statefulset always will be last of the cluster.
## However if the last RabbitMQ of the cluster is not the first RabbitMQ due to a failure,
## you must change podManagementPolicy to 'Parallel'.
## ref : https://www.rabbitmq.com/clustering.html#restarting
## @param podManagementPolicy Pod management policy
##
podManagementPolicy: OrderedReady
## @param podLabels RabbitMQ Pod labels. Evaluated as a template
## Ref: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
##
podLabels: {}
## @param podAnnotations RabbitMQ Pod annotations. Evaluated as a template
## ref: https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
##
podAnnotations: {}
## @param updateStrategy.type Update strategy type for RabbitMQ statefulset
## ref: https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#update-strategies
##
updateStrategy:
  ## StrategyType
  ## Can be set to RollingUpdate or OnDelete
  ##
  type: RollingUpdate
## @param statefulsetLabels RabbitMQ statefulset labels. Evaluated as a template
## Ref: https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
##
statefulsetLabels: {}
## @param priorityClassName Name of the priority class to be used by RabbitMQ pods, priority class needs to be created beforehand
## Ref: https://kubernetes.io/docs/concepts/configuration/pod-priority-preemption/
##
priorityClassName: ""
## @param podAffinityPreset Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`
## ref: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity
##
podAffinityPreset: ""
## @param podAntiAffinityPreset Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`
## Ref: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity
##
podAntiAffinityPreset: soft

## Node affinity preset
## Ref: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity
##
nodeAffinityPreset:
  ## @param nodeAffinityPreset.type Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`
  ##
  type: ""
  ## @param nodeAffinityPreset.key Node label key to match Ignored if `affinity` is set.
  ## E.g.
  ## key: "kubernetes.io/e2e-az-name"
  ##
  key: ""
  ## @param nodeAffinityPreset.values Node label values to match. Ignored if `affinity` is set.
  ## E.g.
  ## values:
  ##   - e2e-az1
  ##   - e2e-az2
  ##
  values: []

## @param affinity Affinity for pod assignment. Evaluated as a template
## Ref: https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity
## Note: podAffinityPreset, podAntiAffinityPreset, and  nodeAffinityPreset will be ignored when it's set
##
affinity: {}
## @param nodeSelector Node labels for pod assignment. Evaluated as a template
## ref: https://kubernetes.io/docs/user-guide/node-selection/
##
nodeSelector: {}
## @param tolerations Tolerations for pod assignment. Evaluated as a template
## Ref: https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/
##
tolerations: []
## @param topologySpreadConstraints Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template
## Ref: https://kubernetes.io/docs/concepts/workloads/pods/pod-topology-spread-constraints/#spread-constraints-for-pods
##
topologySpreadConstraints: []

## RabbitMQ pods' Security Context
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod
## @param podSecurityContext.enabled Enable RabbitMQ pods' Security Context
## @param podSecurityContext.fsGroup Set RabbitMQ pod's Security Context fsGroup
##
podSecurityContext:
  enabled: true
  fsGroup: 1001

## @param containerSecurityContext.enabled Enabled RabbitMQ containers' Security Context
## @param containerSecurityContext.runAsUser Set RabbitMQ containers' Security Context runAsUser
## @param containerSecurityContext.runAsNonRoot Set RabbitMQ container's Security Context runAsNonRoot
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-container
## Example:
##   containerSecurityContext:
##     capabilities:
##       drop: ["NET_RAW"]
##     readOnlyRootFilesystem: true
##
containerSecurityContext:
  enabled: true
  runAsUser: 1001
  runAsNonRoot: true

## RabbitMQ containers' resource requests and limits
## ref: https://kubernetes.io/docs/user-guide/compute-resources/
## We usually recommend not to specify default resources and to leave this as a conscious
## choice for the user. This also increases chances charts run on environments with little
## resources, such as Minikube. If you do want to specify resources, uncomment the following
## lines, adjust them as necessary, and remove the curly braces after 'resources:'.
## @param resources.limits The resources limits for RabbitMQ containers
## @param resources.requests The requested resources for RabbitMQ containers
##
resources:
  ## Example:
  ## limits:
  ##    cpu: 1000m
  ##    memory: 2Gi
  ##
  limits: {}
  ## Examples:
  ## requests:
  ##    cpu: 1000m
  ##    memory: 2Gi
  ##
  requests: {}

## Configure RabbitMQ containers' extra options for liveness probe
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/#configure-probes
## @param livenessProbe.enabled Enable livenessProbe
## @param livenessProbe.initialDelaySeconds Initial delay seconds for livenessProbe
## @param livenessProbe.periodSeconds Period seconds for livenessProbe
## @param livenessProbe.timeoutSeconds Timeout seconds for livenessProbe
## @param livenessProbe.failureThreshold Failure threshold for livenessProbe
## @param livenessProbe.successThreshold Success threshold for livenessProbe
##
livenessProbe:
  enabled: true
  initialDelaySeconds: 120
  timeoutSeconds: 20
  periodSeconds: 30
  failureThreshold: 6
  successThreshold: 1
## Configure RabbitMQ containers' extra options for readiness probe
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/#configure-probes
## @param readinessProbe.enabled Enable readinessProbe
## @param readinessProbe.initialDelaySeconds Initial delay seconds for readinessProbe
## @param readinessProbe.periodSeconds Period seconds for readinessProbe
## @param readinessProbe.timeoutSeconds Timeout seconds for readinessProbe
## @param readinessProbe.failureThreshold Failure threshold for readinessProbe
## @param readinessProbe.successThreshold Success threshold for readinessProbe
##
readinessProbe:
  enabled: true
  initialDelaySeconds: 10
  timeoutSeconds: 20
  periodSeconds: 30
  failureThreshold: 3
  successThreshold: 1

## Configure RabbitMQ containers' extra options for startup probe
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/#configure-probes
## @param startupProbe.enabled Enable startupProbe
## @param startupProbe.initialDelaySeconds Initial delay seconds for startupProbe
## @param startupProbe.periodSeconds Period seconds for startupProbe
## @param startupProbe.timeoutSeconds Timeout seconds for startupProbe
## @param startupProbe.failureThreshold Failure threshold for startupProbe
## @param startupProbe.successThreshold Success threshold for startupProbe
##
startupProbe:
  enabled: false
  initialDelaySeconds: 10
  timeoutSeconds: 20
  periodSeconds: 30
  failureThreshold: 3
  successThreshold: 1

## @param customLivenessProbe Override default liveness probe
##
customLivenessProbe: {}
## @param customReadinessProbe Override default readiness probe
##
customReadinessProbe: {}
## @param customStartupProbe Define a custom startup probe
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes
##
customStartupProbe: {}
## @param initContainers Add init containers to the RabbitMQ pod
## Example:
## initContainers:
##   - name: your-image-name
##     image: your-image
##     imagePullPolicy: Always
##     ports:
##       - name: portname
##         containerPort: 1234
##
initContainers: []
## @param sidecars Add sidecar containers to the RabbitMQ pod
## Example:
## sidecars:
##   - name: your-image-name
##     image: your-image
##     imagePullPolicy: Always
##     ports:
##       - name: portname
##         containerPort: 1234
##
sidecars: []

## Pod Disruption Budget configuration
## ref: https://kubernetes.io/docs/tasks/run-application/configure-pdb/
##
pdb:
  ## @param pdb.create Enable/disable a Pod Disruption Budget creation
  ##
  create: false
  ## @param pdb.minAvailable Minimum number/percentage of pods that should remain scheduled
  ##
  minAvailable: 1
  ## @param pdb.maxUnavailable Maximum number/percentage of pods that may be made unavailable
  ##
  maxUnavailable: ""

## @section RBAC parameters
##

## RabbitMQ pods ServiceAccount
## ref: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
##
serviceAccount:
  ## @param serviceAccount.create Enable creation of ServiceAccount for RabbitMQ pods
  ##
  create: true
  ## @param serviceAccount.name Name of the created serviceAccount
  ## If not set and create is true, a name is generated using the rabbitmq.fullname template
  ##
  name: ""
  ## @param serviceAccount.automountServiceAccountToken Auto-mount the service account token in the pod
  ##
  automountServiceAccountToken: true
  ## @param serviceAccount.annotations Annotations for service account. Evaluated as a template. Only used if `create` is `true`.
  ##
  annotations: {}

## Role Based Access
## ref: https://kubernetes.io/docs/admin/authorization/rbac/
##
rbac:
  ## @param rbac.create Whether RBAC rules should be created
  ## binding RabbitMQ ServiceAccount to a role
  ## that allows RabbitMQ pods querying the K8s API
  ##
  create: true

## @section Persistence parameters
##

persistence:
  ## @param persistence.enabled Enable RabbitMQ data persistence using PVC
  ##
  enabled: true
  ## @param persistence.storageClass PVC Storage Class for RabbitMQ data volume
  ## If defined, storageClassName: <storageClass>
  ## If set to "-", storageClassName: "", which disables dynamic provisioning
  ## If undefined (the default) or set to null, no storageClassName spec is
  ##   set, choosing the default provisioner.  (gp2 on AWS, standard on
  ##   GKE, AWS & OpenStack)
  ##
  storageClass: ""
  ## @param persistence.selector Selector to match an existing Persistent Volume
  ## selector:
  ##   matchLabels:
  ##     app: my-app
  ##
  selector: {}
  ## @param persistence.accessModes PVC Access Modes for RabbitMQ data volume
  ##
  accessModes:
    - ReadWriteOnce
  ## @param persistence.existingClaim Provide an existing PersistentVolumeClaims
  ## The value is evaluated as a template
  ## So, for example, the name can depend on .Release or .Chart
  ##
  existingClaim: ""
  ## @param persistence.mountPath The path the volume will be mounted at
  ## Note: useful when using custom RabbitMQ images
  ##
  mountPath: /bitnami/rabbitmq/mnesia
  ## @param persistence.subPath The subdirectory of the volume to mount to
  ## Useful in dev environments and one PV for multiple services
  ##
  subPath: ""
  ## @param persistence.size PVC Storage Request for RabbitMQ data volume
  ## If you change this value, you might have to adjust `rabbitmq.diskFreeLimit` as well
  ##
  size: 8Gi
  ## @param persistence.annotations Persistence annotations. Evaluated as a template
  ## Example:
  ## annotations:
  ##   example.io/disk-volume-type: SSD
  ##
  annotations: {}

## @section Exposure parameters
##

## Kubernetes service type
##
service:
  ## @param service.type Kubernetes Service type
  ##
  type: ClusterIP

  ## @param service.portEnabled Amqp port. Cannot be disabled when `auth.tls.enabled` is `false`. Listener can be disabled with `listeners.tcp = none`.
  ##
  portEnabled: true
  ## @param service.distPortEnabled Erlang distribution server port
  ##
  distPortEnabled: true
  ## @param service.managerPortEnabled RabbitMQ Manager port
  ## ref: https://github.com/bitnami/containers/tree/main/bitnami/rabbitmq#environment-variables
  ##
  managerPortEnabled: true
  ## @param service.epmdPortEnabled RabbitMQ EPMD Discovery service port
  ##
  epmdPortEnabled: true
  ## Service ports
  ## @param service.ports.amqp Amqp service port
  ## @param service.ports.amqpTls Amqp TLS service port
  ## @param service.ports.dist Erlang distribution service port
  ## @param service.ports.manager RabbitMQ Manager service port
  ## @param service.ports.metrics RabbitMQ Prometheues metrics service port
  ## @param service.ports.epmd EPMD Discovery service port
  ##
  ports:
    amqp: 5672
    amqpTls: 5671
    dist: 25672
    manager: 15672
    metrics: 9419
    epmd: 4369
  ## Service ports name
  ## @param service.portNames.amqp Amqp service port name
  ## @param service.portNames.amqpTls Amqp TLS service port name
  ## @param service.portNames.dist Erlang distribution service port name
  ## @param service.portNames.manager RabbitMQ Manager service port name
  ## @param service.portNames.metrics RabbitMQ Prometheues metrics service port name
  ## @param service.portNames.epmd EPMD Discovery service port name
  ##
  portNames:
    amqp: "amqp"
    amqpTls: "amqp-ssl"
    dist: "dist"
    manager: "http-stats"
    metrics: "metrics"
    epmd: "epmd"

  ## Node ports to expose
  ## @param service.nodePorts.amqp Node port for Ampq
  ## @param service.nodePorts.amqpTls Node port for Ampq TLS
  ## @param service.nodePorts.dist Node port for Erlang distribution
  ## @param service.nodePorts.manager Node port for RabbitMQ Manager
  ## @param service.nodePorts.epmd Node port for EPMD Discovery
  ## @param service.nodePorts.metrics Node port for RabbitMQ Prometheues metrics
  ##
  nodePorts:
    amqp: ""
    amqpTls: ""
    dist: ""
    manager: ""
    epmd: ""
    metrics: ""
  ## @param service.extraPorts Extra ports to expose in the service
  ## E.g.:
  ## extraPorts:
  ## - name: new_svc_name
  ##   port: 1234
  ##   targetPort: 1234
  ##
  extraPorts: []
  ## @param service.loadBalancerSourceRanges Address(es) that are allowed when service is `LoadBalancer`
  ## https://kubernetes.io/docs/tasks/access-application-cluster/configure-cloud-provider-firewall/#restrict-access-for-loadbalancer-service
  ## e.g:
  ## loadBalancerSourceRanges:
  ## - 10.10.10.0/24
  ##
  loadBalancerSourceRanges: []
  ## @param service.externalIPs Set the ExternalIPs
  ##
  externalIPs: []
  ## @param service.externalTrafficPolicy Enable client source IP preservation
  ## ref https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip
  ##
  externalTrafficPolicy: Cluster
  ## @param service.loadBalancerIP Set the LoadBalancerIP
  ##
  loadBalancerIP: ""
  ## @param service.clusterIP Kubernetes service Cluster IP
  ## e.g.:
  ## clusterIP: None
  ##
  clusterIP: ""
  ## @param service.labels Service labels. Evaluated as a template
  ##
  labels: {}
  ## @param service.annotations Service annotations. Evaluated as a template
  ## Example:
  ## annotations:
  ##   service.beta.kubernetes.io/aws-load-balancer-internal: 0.0.0.0/0
  ##
  annotations: {}
  ## @param service.annotationsHeadless Headless Service annotations. Evaluated as a template
  ## Example:
  ## annotations:
  ##   external-dns.alpha.kubernetes.io/internal-hostname: rabbitmq.example.com
  ##
  annotationsHeadless: {}
  ## @param service.sessionAffinity Session Affinity for Kubernetes service, can be "None" or "ClientIP"
  ## If "ClientIP", consecutive client requests will be directed to the same Pod
  ## ref: https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies
  ##
  sessionAffinity: None
  ## @param service.sessionAffinityConfig Additional settings for the sessionAffinity
  ## sessionAffinityConfig:
  ##   clientIP:
  ##     timeoutSeconds: 300
  ##
  sessionAffinityConfig: {}

## Configure the ingress resource that allows you to access the
## RabbitMQ installation. Set up the URL
## ref: https://kubernetes.io/docs/user-guide/ingress/
##
ingress:
  ## @param ingress.enabled Enable ingress resource for Management console
  ##
  enabled: false

  ## @param ingress.path Path for the default host. You may need to set this to '/*' in order to use this with ALB ingress controllers.
  ##
  path: /

  ## @param ingress.pathType Ingress path type
  ##
  pathType: ImplementationSpecific
  ## @param ingress.hostname Default host for the ingress resource
  ##
  hostname: rabbitmq.local
  ## @param ingress.annotations Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations.
  ## For a full list of possible ingress annotations, please see
  ## ref: https://github.com/kubernetes/ingress-nginx/blob/master/docs/user-guide/nginx-configuration/annotations.md
  ## Use this parameter to set the required annotations for cert-manager, see
  ## ref: https://cert-manager.io/docs/usage/ingress/#supported-annotations
  ##
  ## e.g:
  ## annotations:
  ##   kubernetes.io/ingress.class: nginx
  ##   cert-manager.io/cluster-issuer: cluster-issuer-name
  ##
  annotations: {}
  ## @param ingress.tls Enable TLS configuration for the hostname defined at `ingress.hostname` parameter
  ## TLS certificates will be retrieved from a TLS secret with name: {{- printf "%s-tls" .Values.ingress.hostname }}
  ## You can:
  ##   - Use the `ingress.secrets` parameter to create this TLS secret
  ##   - Rely on cert-manager to create it by setting the corresponding annotations
  ##   - Rely on Helm to create self-signed certificates by setting `ingress.selfSigned=true`
  ##
  tls: false
  ## @param ingress.selfSigned Set this to true in order to create a TLS secret for this ingress record
  ## using self-signed certificates generated by Helm
  ##
  selfSigned: false
  ## @param ingress.extraHosts The list of additional hostnames to be covered with this ingress record.
  ## Most likely the hostname above will be enough, but in the event more hosts are needed, this is an array
  ## e.g:
  ## extraHosts:
  ##   - name: rabbitmq.local
  ##     path: /
  ##
  extraHosts: []
  ## @param ingress.extraPaths An array with additional arbitrary paths that may need to be added to the ingress under the main host
  ## e.g:
  ## extraPaths:
  ## - path: /*
  ##   backend:
  ##     serviceName: ssl-redirect
  ##     servicePort: use-annotation
  ##
  extraPaths: []
  ## @param ingress.extraRules The list of additional rules to be added to this ingress record. Evaluated as a template
  ## Useful when looking for additional customization, such as using different backend
  ##
  extraRules: []
  ## @param ingress.extraTls The tls configuration for additional hostnames to be covered with this ingress record.
  ## see: https://kubernetes.io/docs/concepts/services-networking/ingress/#tls
  ## e.g:
  ## extraTls:
  ##   - hosts:
  ##       - rabbitmq.local
  ##     secretName: rabbitmq.local-tls
  ##
  extraTls: []
  ## @param ingress.secrets Custom TLS certificates as secrets
  ## NOTE: 'key' and 'certificate' are expected in PEM format
  ## NOTE: 'name' should line up with a 'secretName' set further up
  ## If it is not set and you're using cert-manager, this is unneeded, as it will create a secret for you with valid certificates
  ## If it is not set and you're NOT using cert-manager either, self-signed certificates will be created valid for 365 days
  ## It is also possible to create and manage the certificates outside of this helm chart
  ## Please see README.md for more information
  ## e.g:
  ## secrets:
  ##   - name: rabbitmq.local-tls
  ##     key: |-
  ##       -----BEGIN RSA PRIVATE KEY-----
  ##       ...
  ##       -----END RSA PRIVATE KEY-----
  ##     certificate: |-
  ##       -----BEGIN CERTIFICATE-----
  ##       ...
  ##       -----END CERTIFICATE-----
  ##
  secrets: []
  ## @param ingress.ingressClassName IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)
  ## This is supported in Kubernetes 1.18+ and required if you have more than one IngressClass marked as the default for your cluster .
  ## ref: https://kubernetes.io/blog/2020/04/02/improvements-to-the-ingress-api-in-kubernetes-1.18/
  ##
  ingressClassName: ""

## Network Policy configuration
## ref: https://kubernetes.io/docs/concepts/services-networking/network-policies/
##
networkPolicy:
  ## @param networkPolicy.enabled Enable creation of NetworkPolicy resources
  ##
  enabled: false
  ## @param networkPolicy.allowExternal Don't require client label for connections
  ## The Policy model to apply. When set to false, only pods with the correct
  ## client label will have network access to the ports RabbitMQ is listening
  ## on. When true, RabbitMQ will accept connections from any source
  ## (with the correct destination port).
  ##
  allowExternal: true
  ## @param networkPolicy.additionalRules Additional NetworkPolicy Ingress "from" rules to set. Note that all rules are OR-ed.
  ## e.g:
  ## additionalRules:
  ##  - matchLabels:
  ##    - role: frontend
  ##  - matchExpressions:
  ##    - key: role
  ##      operator: In
  ##      values:
  ##        - frontend
  ##
  additionalRules: []

## @section Metrics Parameters
##

## Prometheus Metrics
##
metrics:
  ## @param metrics.enabled Enable exposing RabbitMQ metrics to be gathered by Prometheus
  ##
  enabled: false
  ## @param metrics.plugins Plugins to enable Prometheus metrics in RabbitMQ
  ##
  plugins: "rabbitmq_prometheus"
  ## Prometheus pod annotations
  ## @param metrics.podAnnotations [object] Annotations for enabling prometheus to access the metrics endpoint
  ## ref: https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/
  ##
  podAnnotations:
    prometheus.io/scrape: "true"
    prometheus.io/port: "{{ .Values.service.ports.metrics }}"
  ## Prometheus Service Monitor
  ## ref: https://github.com/coreos/prometheus-operator
  ##
  serviceMonitor:
    ## @param metrics.serviceMonitor.enabled Create ServiceMonitor Resource for scraping metrics using PrometheusOperator
    ##
    enabled: false
    ## @param metrics.serviceMonitor.namespace Specify the namespace in which the serviceMonitor resource will be created
    ##
    namespace: ""
    ## @param metrics.serviceMonitor.interval Specify the interval at which metrics should be scraped
    ##
    interval: 30s
    ## @param metrics.serviceMonitor.scrapeTimeout Specify the timeout after which the scrape is ended
    ## e.g:
    ## scrapeTimeout: 30s
    ##
    scrapeTimeout: ""
    ## @param metrics.serviceMonitor.jobLabel The name of the label on the target service to use as the job name in prometheus.
    ##
    jobLabel: ""
    ## @param metrics.serviceMonitor.relabelings RelabelConfigs to apply to samples before scraping.
    ##
    relabelings: []
    ## @param metrics.serviceMonitor.metricRelabelings MetricsRelabelConfigs to apply to samples before ingestion.
    ##
    metricRelabelings: []
    ## @param metrics.serviceMonitor.honorLabels honorLabels chooses the metric's labels on collisions with target labels
    ##
    honorLabels: false
    ## @param metrics.serviceMonitor.targetLabels Used to keep given service's labels in target
    ## e.g:
    ## - app.kubernetes.io/name
    ##
    targetLabels: {}
    ## @param metrics.serviceMonitor.podTargetLabels Used to keep given pod's labels in target
    ## e.g:
    ## - app.kubernetes.io/name
    ##
    podTargetLabels: {}
    ## @param metrics.serviceMonitor.path Define the path used by ServiceMonitor to scrap metrics
    ## Could be /metrics for aggregated metrics or /metrics/per-object for more details
    ##
    path: ""
    ## @param metrics.serviceMonitor.selector ServiceMonitor selector labels
    ## ref: https://github.com/bitnami/charts/tree/master/bitnami/prometheus-operator#prometheus-configuration
    ##
    ## selector:
    ##   prometheus: my-prometheus
    ##
    selector: {}
    ## @param metrics.serviceMonitor.labels Extra labels for the ServiceMonitor
    ##
    labels: {}
    ## @param metrics.serviceMonitor.annotations Extra annotations for the ServiceMonitor
    ##
    annotations: {}

  ## Custom PrometheusRule to be defined
  ## The value is evaluated as a template, so, for example, the value can depend on .Release or .Chart
  ## ref: https://github.com/coreos/prometheus-operator#customresourcedefinitions
  ##
  prometheusRule:
    ## @param metrics.prometheusRule.enabled Set this to true to create prometheusRules for Prometheus operator
    ##
    enabled: false
    ## @param metrics.prometheusRule.additionalLabels Additional labels that can be used so prometheusRules will be discovered by Prometheus
    ##
    additionalLabels: {}
    ## @param metrics.prometheusRule.namespace namespace where prometheusRules resource should be created
    ##
    namespace: ""
    ## List of rules, used as template by Helm.
    ## @param metrics.prometheusRule.rules List of rules, used as template by Helm.
    ## These are just examples rules inspired from https://awesome-prometheus-alerts.grep.to/rules.html
    ## rules:
    ##   - alert: RabbitmqDown
    ##     expr: rabbitmq_up{service="{{ template "common.names.fullname" . }}"} == 0
    ##     for: 5m
    ##     labels:
    ##       severity: error
    ##     annotations:
    ##       summary: Rabbitmq down (instance {{ "{{ $labels.instance }}" }})
    ##       description: RabbitMQ node down
    ##   - alert: ClusterDown
    ##     expr: |
    ##       sum(rabbitmq_running{service="{{ template "common.names.fullname" . }}"})
    ##       < {{ .Values.replicaCount }}
    ##     for: 5m
    ##     labels:
    ##       severity: error
    ##     annotations:
    ##       summary: Cluster down (instance {{ "{{ $labels.instance }}" }})
    ##       description: |
    ##           Less than {{ .Values.replicaCount }} nodes running in RabbitMQ cluster
    ##           VALUE = {{ "{{ $value }}" }}
    ##   - alert: ClusterPartition
    ##     expr: rabbitmq_partitions{service="{{ template "common.names.fullname" . }}"} > 0
    ##     for: 5m
    ##     labels:
    ##       severity: error
    ##     annotations:
    ##       summary: Cluster partition (instance {{ "{{ $labels.instance }}" }})
    ##       description: |
    ##           Cluster partition
    ##           VALUE = {{ "{{ $value }}" }}
    ##   - alert: OutOfMemory
    ##     expr: |
    ##       rabbitmq_node_mem_used{service="{{ template "common.names.fullname" . }}"}
    ##       / rabbitmq_node_mem_limit{service="{{ template "common.names.fullname" . }}"}
    ##       * 100 > 90
    ##     for: 5m
    ##     labels:
    ##       severity: warning
    ##     annotations:
    ##       summary: Out of memory (instance {{ "{{ $labels.instance }}" }})
    ##       description: |
    ##           Memory available for RabbmitMQ is low (< 10%)\n  VALUE = {{ "{{ $value }}" }}
    ##           LABELS: {{ "{{ $labels }}" }}
    ##   - alert: TooManyConnections
    ##     expr: rabbitmq_connectionsTotal{service="{{ template "common.names.fullname" . }}"} > 1000
    ##     for: 5m
    ##     labels:
    ##       severity: warning
    ##     annotations:
    ##       summary: Too many connections (instance {{ "{{ $labels.instance }}" }})
    ##       description: |
    ##           RabbitMQ instance has too many connections (> 1000)
    ##           VALUE = {{ "{{ $value }}" }}\n  LABELS: {{ "{{ $labels }}" }}
    ##
    rules: []

## @section Init Container Parameters
##

## Init Container parameters
## Change the owner and group of the persistent volume(s) mountpoint(s) to 'runAsUser:fsGroup' on each component
## values from the securityContext section of the component
##
volumePermissions:
  ## @param volumePermissions.enabled Enable init container that changes the owner and group of the persistent volume(s) mountpoint to `runAsUser:fsGroup`
  ##
  enabled: false
  ## @param volumePermissions.image.registry Init container volume-permissions image registry
  ## @param volumePermissions.image.repository Init container volume-permissions image repository
  ## @param volumePermissions.image.tag Init container volume-permissions image tag
  ## @param volumePermissions.image.digest Init container volume-permissions image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag
  ## @param volumePermissions.image.pullPolicy Init container volume-permissions image pull policy
  ## @param volumePermissions.image.pullSecrets Specify docker-registry secret names as an array
  ##
  image:
    registry: docker.io
    repository: bitnami/bitnami-shell
    tag: 11-debian-11-r38
    digest: ""
    ## Specify a imagePullPolicy
    ## Defaults to 'Always' if image tag is 'latest', else set to 'IfNotPresent'
    ## ref: https://kubernetes.io/docs/user-guide/images/#pre-pulling-images
    ##
    pullPolicy: IfNotPresent
    ## Optionally specify an array of imagePullSecrets (secrets must be manually created in the namespace)
    ## ref: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
    ## Example:
    ## pullSecrets:
    ##   - myRegistryKeySecretName
    ##
    pullSecrets: []
  ## Init Container resource requests and limits
  ## ref: https://kubernetes.io/docs/user-guide/compute-resources/
  ## We usually recommend not to specify default resources and to leave this as a conscious
  ## choice for the user. This also increases chances charts run on environments with little
  ## resources, such as Minikube. If you do want to specify resources, uncomment the following
  ## lines, adjust them as necessary, and remove the curly braces after 'resources:'.
  ## @param volumePermissions.resources.limits Init container volume-permissions resource limits
  ## @param volumePermissions.resources.requests Init container volume-permissions resource requests
  ##
  resources:
    ## Example:
    ## limits:
    ##    cpu: 100m
    ##    memory: 128Mi
    ##
    limits: {}
    ## Examples:
    ## requests:
    ##    cpu: 100m
    ##    memory: 128Mi
    ##
    requests: {}
  ## Init container' Security Context
  ## Note: the chown of the data folder is done to containerSecurityContext.runAsUser
  ## and not the below volumePermissions.containerSecurityContext.runAsUser
  ## @param volumePermissions.containerSecurityContext.runAsUser User ID for the init container
  ##
  containerSecurityContext:
    runAsUser: 0

```
