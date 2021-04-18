# GCP にてホスティング出来るようにする

+ Cloud SQL for PostgreSQL のインスタンスを作成する

```
export _sql_instance_name='liff-todo-app'
export _root_passwd='Your PostgreSQL Admin User Password'
export _gcp_pj_id='Your GCP Project ID'


gcloud beta sql instances create ${_sql_instance_name} \
  --database-version POSTGRES_9_6 \
  --root-password=${_root_passwd} \
  --tier db-f1-micro \
  --region asia-northeast1 \
  --project ${_gcp_pj_id}
```

+ 使っていない時は一時停止させておく

```
gcloud beta sql instances patch ${_sql_instance_name} \
    --activation-policy NEVER \
    --project ${_gcp_pj_id}
```

+ 停止状態からの起動

```
gcloud beta sql instances patch ${_sql_instance_name} \
    --activation-policy ALWAYS \
    --project ${_gcp_pj_id}
```


+ [予定] 削除

```
gcloud beta sql instances delete ${_sql_instance_name}  \
  --project ${_gcp_pj_id} \
  -q
```

## App Engine から Cloud SQL につなぐ

https://cloud.google.com/sql/docs/mysql/connect-app-engine-standard#public-ip-default
