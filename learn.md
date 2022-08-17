k3s = kubectl + kubeadm

main.go 程序入口


// server相关数据结构
//pkg/cli/cmds/server.go 

var (
	ServerConfig Server			// 从cli、配置文件加载配置参数
)

type Server struct {

	ClusterCIDR          cli.StringSlice	// (networking) IPv4/IPv6 network CIDRs to use for pod IPs (default: 10.42.0.0/16) 定义pod 使用的（虚拟）网段的参数
	
	AgentToken           string		// (cluster) Shared secret used to join agents to the cluster, but not servers. 将k8s worker node加入k8s cluster的命令：kubeadm join --discovery-token abcdef.1234567890abcdef
	
	AgentTokenFile       string		// File containing the agent secret
	
	Token                string		// Shared secret used to join a server or agent to a cluster. 将一个k8s server node加入k8s cluster的命令
	
	TokenFile            string		// (cluster) File containing the cluster-secret/token
	
	ClusterSecret        string
	
	ServiceCIDR          cli.StringSlice  // service 使用的网段
	ServiceNodePortRange string           // service 独占的端口范围（默认：30000-32767）
	ClusterDNS           cli.StringSlice  // IPv4 Cluster IP for coredns service. Should be in your service-cidr range (default: 10.43.0.10)
	ClusterDomain        string     // 集群域名（默认：cluster.local）
	// The port which kubectl clients can access k8s
	HTTPSPort int
	// The port which custom k3s API runs on
	SupervisorPort int
	// The port which kube-apiserver runs on
	APIServerPort            int
	APIServerBindAddress     string
	
	DataDir                  string  // k3s 进程top目录
	
	DisableAgent             bool    // true: 运行在k3s master模式;  false: 运行在k3s master 和 k3s worker模式
	KubeConfigOutput         string  // kubeadm init 生成的配置文件文件存储路径
	KubeConfigMode           string  // 文件读写模式
	
	TLSSan                   cli.StringSlice
	BindAddress              string  // bind address (default: 0.0.0.0)
	ExtraAPIArgs             cli.StringSlice  // m3s master rest api 监听端口
	ExtraEtcdArgs            cli.StringSlice  // m3s master etcd数据库扩展参数
	ExtraSchedulerArgs       cli.StringSlice  // 资源调度器(监测集群node资源)扩展参数
	ExtraControllerArgs      cli.StringSlice  // 资源控制器（监测集群定义资源，并触发资源调度）扩展参数
	ExtraCloudControllerArgs cli.StringSlice  // 多地k3s cluster 协同参数
	
	Rootless                 bool    // k3s以非root权限运行
	
	DatastoreEndpoint        string
	DatastoreCAFile          string
	DatastoreCertFile        string
	DatastoreKeyFile         string
	
	AdvertiseIP              string
	AdvertisePort            int
	
	DisableScheduler         bool    // pause k3s资源调度
	ServerURL                string
	FlannelBackend           string  // k3s 网络插件
	FlannelIPv6Masq          bool
	DefaultLocalStoragePath  string  // pv卷默认存储路径
	DisableCCM               bool    // 禁止ccm鉴权模块
	DisableNPC               bool
	DisableHelmController    bool    // 禁止helm工具入口
	DisableKubeProxy         bool    // 禁止使用Kubeproxy
	DisableAPIServer         bool
	DisableControllerManager bool    // 禁止k3s 执行新的调度
	DisableETCD              bool
	
	ClusterInit              bool    // 执行kubeadm init ，创建集群map文件
	ClusterReset             bool    // kubeadm reset，删除集群map文件
	ClusterResetRestorePath  string

    // ssl加密通讯
	EncryptSecrets           bool
	EncryptForce             bool
	EncryptOutput            string
	EncryptSkip              bool
	
	SystemDefaultRegistry    string
	StartupHooks             []StartupHook  // 指定k3s启动后需要执行的钩子函数
   
    // etcd数据库相关参数（访问端点、访问账号、etcd备份周期、备份文件是否压缩）
	EtcdSnapshotName         string
	EtcdDisableSnapshots     bool
	EtcdExposeMetrics        bool
	EtcdSnapshotDir          string
	EtcdSnapshotCron         string
	EtcdSnapshotRetention    int
	EtcdSnapshotCompress     bool
	EtcdListFormat           string
	EtcdS3                   bool
	EtcdS3Endpoint           string
	EtcdS3EndpointCA         string
	EtcdS3SkipSSLVerify      bool
	EtcdS3AccessKey          string
	EtcdS3SecretKey          string
	EtcdS3BucketName         string
	EtcdS3Region             string
	EtcdS3Folder             string
	EtcdS3Timeout            time.Duration
	EtcdS3Insecure           bool
}

