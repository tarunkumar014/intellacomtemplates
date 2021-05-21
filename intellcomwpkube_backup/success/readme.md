define( 'S3_UPLOADS_BUCKET', 'intellaspherecom');
define( 'S3_UPLOADS_KEY', '87d4L3FWsXV7a5DqoG9a');
define( 'S3_UPLOADS_SECRET', 'CNvsIAZxGaC8TmilUYyeZq11oTmMGb8evCBqTfOS');
define( 'S3_UPLOADS_BUCKET_CDN_URL', 'https://cdn.lsnsoftinc.com');
define( 'S3_UPLOADS_BUCKET_URL', 'https://cdn.lsnsoftinc.com');
define( 'S3_UPLOADS_REGION', 'us' );



$params['endpoint'] = 'https://minio2.intellasphere.com/minio






































































apiVersion: v1
kind: Pod
metadata:
  annotations:
    cni.projectcalico.org/podIP: 10.68.10.236/32
  creationTimestamp: "2021-05-20T13:04:22Z"
  generateName: wordpress-nginx-7dff7cd45b-
  labels:
    app: wordpress-nginx
    pod-template-hash: 7dff7cd45b
  name: wordpress-nginx-7dff7cd45b-9znl6
  namespace: devintellapages
  ownerReferences:
  - apiVersion: apps/v1
    blockOwnerDeletion: true
    controller: true
    kind: ReplicaSet
    name: wordpress-nginx-7dff7cd45b
    uid: c3eb4400-274e-4e23-abcb-66db6b3ace3b
  resourceVersion: "82539418"
  selfLink: /api/v1/namespaces/devintellapages/pods/wordpress-nginx-7dff7cd45b-9znl6
  uid: 91ee4a41-1e55-4172-9d40-5d8df662827f
spec:
  containers:
  - env:
    - name: WORDPRESS_DB_HOST
      value: 10.25.128.2
    - name: WORDPRESS_DB_USER
      value: intellacomwordpress
    - name: WORDPRESS_DB_PASSWORD
      value: oteo0buZooPei0ebeiphoo
    - name: WORDPRESS_DB_NAME
      value: intellacomwordpress
    - name: WORDPRESS_TABLE_PREFIX
      value: wp_
    - name: WORDPRESS_AUTH_KEY
      value: -N#h4L)4L(|iXj3jJdZ^}H]-ubXOEVtk^kp-[|HzmU||d8Y/xtY&iAa:zNIxbiO%
    - name: WORDPRESS_SECURE_AUTH_KEY
      value: ;O8wAE=L5~x>8we2jX5Q;cp1_DYXJVLm1*W^6V3I<)9-^`j`.~@fode&o4*jS>&+
    - name: WORDPRESS_LOGGED_IN_KEY
      value: zb4w=B1gQ}Oe+9ZZ]3|68x9M(#q$?Q9hK*s~HF&Tqb5Za)M;eW_6<+szGGr~ss)=
    - name: WORDPRESS_NONCE_KEY
      value: luYh>&051THe3@8XrJ}H4z xV]U/0$l~V>4rMJ-$mTw%}|EA~f>nP;G5F:].~{{+
    - name: WORDPRESS_AUTH_SALT
      value: '`.1}wH>aCj4<V_9X^!G,yI2-lX5+i&+KsP&=&[Iz{2]?%R,2cdXSxQ{~/mT|;yb6'
    - name: WORDPRESS_SECURE_AUTH_SALT
      value: r;Jg(E7!=H3K+@(k@ttC[D_(, gpN28ScU<,Ry-zz~-~!AWAnU7UQ,&c4jOMf(XD
    - name: WORDPRESS_LOGGED_IN_SALT
      value: iff66Kj<N_(FfGL8+)JK3t5-4B*xabfyj)-yyUJO%a J:1)O#$X2%/0ubv=;.p-c
    - name: WORDPRESS_NONCE_SALT
      value: 2kTd+SKr@_<RJi$>,Q.7 $bav_3|oc<6VE?PNl|ZeqC$[lQ<HE)r0by5`X,7P?]e
    - name: WORDPRESS_CONFIG_EXTRA
      valueFrom:
        configMapKeyRef:
          key: wordpress-extraconfig
          name: wordpress-extraconfig
    image: intellasphere.azurecr.io/intellaspherecom:v5
    imagePullPolicy: Always
    name: wordpress-fpm-alpine
    ports:
    - containerPort: 9000
      protocol: TCP
    resources:
      requests:
        cpu: 300m
        memory: 200Mi
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/www/html
      name: shared-data-dir
    - mountPath: /root/.ssh/
      name: trusted-keys
    - mountPath: /root/composermount
      name: composerfile
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-tzqk2
      readOnly: true
  - image: intellasphere.azurecr.io/nginxlive:v2
    imagePullPolicy: Always
    name: nginx
    ports:
    - containerPort: 80
      name: http
      protocol: TCP
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/www/html
      name: shared-data-dir
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: default-token-tzqk2
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  imagePullSecrets:
  - name: teja-azure-container-registry
  nodeName: gke-intellasphere-us-default-pool-a7d4fe0e-cnam
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: shared-data-dir
  - configMap:
      defaultMode: 384
      items:
      - key: id_rsa
        path: id_rsa
      - key: known_hosts
        path: known_hosts
      name: wordpress-gitlab-ssh-key
    name: trusted-keys
  - configMap:
      defaultMode: 420
      items:
      - key: composer.json
        path: composer.json
      name: wordpress-multisite-composerfile
    name: composerfile
  - name: default-token-tzqk2
    secret:
      defaultMode: 420
      secretName: default-token-tzqk2
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2021-05-20T13:04:22Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2021-05-20T13:04:24Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2021-05-20T13:04:24Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2021-05-20T13:04:22Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://30d018e45f15ddbf089709d38ec739abae0b5a72056fb6db55cbac4444fc18cf
    image: intellasphere.azurecr.io/nginxlive:v2
    imageID: docker-pullable://intellasphere.azurecr.io/nginxlive@sha256:1cdedf1b43a09fe750984989ebada5dd76d89338c5c6f921d14e38eb19989bca
    lastState: {}
    name: nginx
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2021-05-20T13:04:24Z"
  - containerID: docker://dc8b085b4c02e240fe3556c200218d991e9b30b78460d0302a93ee425722f433
    image: intellasphere.azurecr.io/intellaspherecom:v5
    imageID: docker-pullable://intellasphere.azurecr.io/intellaspherecom@sha256:7bf06ea602ce8d7e1c42abc7630cc312d0033f43a8e9a5de217b45197e5bad2f
    lastState: {}
    name: wordpress-fpm-alpine
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2021-05-20T13:04:23Z"
  hostIP: 10.128.15.213
  phase: Running
  podIP: 10.68.10.236
  podIPs:
  - ip: 10.68.10.236
  qosClass: Burstable
  startTime: "2021-05-20T13:04:22Z"
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  <?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the
 * installation. You don't have to use the web site, you can
 * copy this file to "wp-config.php" and fill in the values.
 *
 * This file contains the following configurations:
 *
 * * MySQL settings
 * * Secret keys
 * * Database table prefix
 * * ABSPATH
 *
 * @link https://wordpress.org/support/article/editing-wp-config-php/
 *
 * @package WordPress
 */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'intellacomwordpress');

/** MySQL database username */
define( 'DB_USER', 'intellacomwordpress');

/** MySQL database password */
define( 'DB_PASSWORD', 'oteo0buZooPei0ebeiphoo');

/** MySQL hostname */
define( 'DB_HOST', '10.25.128.2');

/** Database Charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '');

/**#@+
 * Authentication Unique Keys and Salts.
 *
 * Change these to different unique phrases!
 * You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}
 * You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define( 'AUTH_KEY',         '-N#h4L)4L(|iXj3jJdZ^}H]-ubXOEVtk^kp-[|HzmU||d8Y/xtY&iAa:zNIxbiO%');
define( 'SECURE_AUTH_KEY',  ';O8wAE=L5~x>8we2jX5Q;cp1_DYXJVLm1*W^6V3I<)9-^`j`.~@fode&o4*jS>&+');
define( 'LOGGED_IN_KEY',    'zb4w=B1gQ}Oe+9ZZ]3|68x9M(#q$?Q9hK*s~HF&Tqb5Za)M;eW_6<+szGGr~ss)=');
define( 'NONCE_KEY',        'luYh>&051THe3@8XrJ}H4z xV]U/0$l~V>4rMJ-$mTw%}|EA~f>nP;G5F:].~{{+');
define( 'AUTH_SALT',        '`.1}wH>aCj4<V_9X^!G,yI2-lX5+i&+KsP&=&[Iz{2]?%R,2cdXSxQ{~/mT|;yb6');
define( 'SECURE_AUTH_SALT', 'r;Jg(E7!=H3K+@(k@ttC[D_(, gpN28ScU<,Ry-zz~-~!AWAnU7UQ,&c4jOMf(XD');
define( 'LOGGED_IN_SALT',   'iff66Kj<N_(FfGL8+)JK3t5-4B*xabfyj)-yyUJO%a J:1)O#$X2%/0ubv=;.p-c');
define( 'NONCE_SALT',       '2kTd+SKr@_<RJi$>,Q.7 $bav_3|oc<6VE?PNl|ZeqC$[lQ<HE)r0by5`X,7P?]e');

/**#@-*/

/**
 * WordPress Database Table prefix.
 *
 * You can have multiple installations in one database if you give each
 * a unique prefix. Only numbers, letters, and underscores please!
 */
$table_prefix = 'wp_';

/**
 * For developers: WordPress debugging mode.
 *
 * Change this to true to enable the display of notices during development.
 * It is strongly recommended that plugin and theme developers use WP_DEBUG
 * in their development environments.
 *
 * For information on other constants that can be used for debugging,
 * visit the documentation.
 *
 * @link https://wordpress.org/support/article/debugging-in-wordpress/
 */
define( 'WP_DEBUG', false );

// If we're behind a proxy server and using HTTPS, we need to alert WordPress of that fact
// see also http://codex.wordpress.org/Administration_Over_SSL#Using_a_Reverse_Proxy
if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
	$_SERVER['HTTPS'] = 'on';
}

// WORDPRESS_CONFIG_EXTRA
/* w3 total cache */
define( 'WP_CACHE', false /* Modified by NitroPack */ );
define('FS_METHOD','direct');
/* specifying digital ocean keys for s3-uploads */

define( 'S3_UPLOADS_BUCKET', 'intellaspherecom');
define( 'S3_UPLOADS_KEY', '87d4L3FWsXV7a5DqoG9a');
define( 'S3_UPLOADS_SECRET', 'CNvsIAZxGaC8TmilUYyeZq11oTmMGb8evCBqTfOS');
define( 'S3_UPLOADS_BUCKET_CDN_URL', 'https://cdn.lsnsoftinc.com');
define( 'S3_UPLOADS_BUCKET_URL', 'https://cdn.lsnsoftinc.com');
define( 'S3_UPLOADS_REGION', 'us' );


/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
	define( 'ABSPATH', __DIR__ . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';












add_filter( 's3_uploads_s3_client_params', function ( $params ) {
	$params['endpoint'] = 'https://minio2.intellasphere.com/minio';
	$params['use_path_style_endpoint'] = true;
	$params['debug'] = false; // Set to true if uploads are failing.
	return $params;
} );












