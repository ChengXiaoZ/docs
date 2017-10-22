# ����ú�PostgreSQL�ı�����ָ���

### ����
�Գ�

### ����               
2017-10-22

### ��ǩ              
PostgreSQL , ���ݿ�߿��� �� ������ָ�

----

�߿����������ݿ�Ĺؼ�ָ�꣬��˵����Ҫ��������ʱ��̣����ݲ���ʧ���ܹ����˵�ָ��λ�ã�ʱ��/���񣩡�ʵ�ָ߿��õĻ��������ݿ�ı�����ָ�������
  
PostgreSQL������ָ������漰�Ĳ���������ļ��϶࣬�ڲ��߼���ϵ�ϸ��ӣ��ָ����෽ʽ���׻�������Щ����Ӱ�쵽PostgreSQL�߿��÷�����ʵ�֡�

�������Ƚ���ͨ�������ݿ���ϳ����봦������Ȼ��ͨ������PostgreSQL���ݿⱸ����ָ�������ļ���������������Ҫ���̣���PostgreSQL�ָ���ʽ�������������࣬��������Ӧ�Ե��͹��ϣ�PostgreSQL������ָ������÷�����

## һ�����ϳ����ʹ�����
���ݿ���������ļ�����־�ļ����������ݵĴ洢��ʽ��Ϊ������ܣ����ݿ�����ʱ����������λ���ڴ滺�������������������ӳ�д�������ļ�����������ļ��ᴦ�ڲ�һ�µ�״̬�����ݵı����¼��Ϊ��־��¼����־��¼����־�ļ���ʽ�洢�ڴ����ϡ���־��¼Ҳ����д����־����������д����־�ļ���ͨ�������򵥵Ĺ���Write-ahead log��������д�������ļ�ǰ���Ƚ���Ӧ����־��¼д����־�ļ�����Force log at commit�������ύʱ������������־��¼д����־�ļ��������Ա�֤ͨ����־�ļ������Ļָ������ļ���

��ͳ�Ĺ������Ͱ��������ڲ����ϡ�ϵͳ���ϡ����ʣ����̣����ϡ����������ڲ����Ϻ�ϵͳ���ϣ����ݿ�ʹ����־�ļ��Զ��ָ�������Ҫ�˹���Ԥ��ΪӦ�Խ��ʹ��ϣ�DBA�����ȱ������ݣ��������Ϻ�ʹ�ñ������ݻָ����ݿ⡣

�ɿ��Ĵ����豸���Դ�����ͽ��ʹ��ϸ��ʣ������ܼ������ݱ��ݹ�����һ�������Ĺ�������������������޸��˲�Ӧ���޸ĵ����ݡ������ݿ�ĽǶȿ���������������Ĳ�������������Զ��ָ���ֻ��ʹ�ñ������ݲ��ָܻ���ͬʱ���ṩһ��ʱ������ʷ���ݵķ��ʣ�Ҳ��һ������������

���ݵı�����ָ����Է�Ϊ�߼����������ַ�ʽ��
  
* �߼�������ָ�������ʱ��ʹ�ù��߽�����ȫ������Ϊ�ⲿ�ļ����ָ�ʱ��ʹ�ù��ߣ��������ļ������½������ݿ�
  
* ��������ָ�������ʱ������ʵ�����ڹ鵵ģʽ�������ɵ���־�ļ����ֵ�ָ��λ�á�ʹ���ȱ�����ֱ�ӿ������ݵ�����Ŀ¼����Ϊ�������ݡ��ָ�ʱ��ʹ�û������ݺ���־�ļ������ݻָ���һ�µ�״̬��
�߼���ʽ��֧��������ʽ�����������ݽ�С����µı�����ָ�������ʽ֧���������ݣ��ʺϴ��������ı�����ָ�������ֻ������������ָ�����ͼΪ��������ָ��Ļ������̡�

![��������ָ�](media/2017-10-22-How-to-use-PostgreSQL-backup-and-restore-well-1.png)


�ڸ߿��������У�����̨ʵ���������ϣ���Ҫ�����ṩ����ʵ�������ݻ�������+��־�ļ��ķ�ʽ�޷�����ʱ��Ҫ��ͨ������������master/slave��������master��slaveͨ����־�����ƽ���ͬ����slave�����ṩֻ�����ݷ��ʣ���master���͹��Ϻ�ֱ�ӽ�Ӧ������ת����slave��

![����������־�л�](media/2017-10-22-How-to-use-PostgreSQL-backup-and-restore-well-2.png)

�ڸ߿��÷����У���Ҫ֧�ֽ��ʹ��ϻָ���ʵʱ�����л�����������ݻָ����鿴��ʷ���ݵȹ��ܡ������Ƽ�������������ָ��Ľ�ϣ������������ݿ�߿��õĻ���Ҫ��


||������|��������ָ�
---|---|---
���ʹ��ϻָ�|֧��|֧��
ʵʱ�����л�|֧��|��֧��
��������ݻָ�|��֧��|֧��
�鿴��ʷ����|��֧��|֧��


## ����PostgreSQL������ָ�����ļ���������������Ҫ����
### 1.PostgreSQL��־�ļ�������

��־��� (lsn:log sequence number) ��ʶ��־��¼����־�ļ��е�λ�á�lsn��һ��64λ��������PostgreSQL����ʱ���ɵ���־�ļ����������Ŀ¼�µ�pg_xlogĿ¼��ÿ����־�ļ���Ϊһ��segment����־�ļ���С�̶�����wal_segment_size����ָ������־�ļ��ڲ�����Ϊ���wal page��ÿ��page�Ĵ�С��wal_block_size����ָ����

����һ��64λ��lsn�����Լ���������ڵ�xlog�ļ�����lsn���Ի���segment��Ÿ�λ��segment��ŵ�λ�Ϳ�������������֡�����segment��СΪ64M��16M��������£�

16M��segment��Ÿ�λ��32���أ�+segment��ŵ�λ��8���أ�+������ţ�24���أ�

64M��segment��Ÿ�λ��32���أ�+segment��ŵ�λ��6���أ�+������ţ�26���أ�

Xlog�ļ�������������ɣ���ʽΪ��ʱ����+segment��Ÿ�λ+segment��ŵ�λ��ÿ�����ֶ���ʾΪһ��8λ16�������֡�ȡ��lsn�е�segment��λ��segment��λ��ֵ���Ϳ���ȷ�������ڵ�xlog�ļ���

ʹ��pg_current_xlog_location()��ѯ��ǰlsnΪ0/1C000090��16���Ƹ�32λ/16���Ƶ�32λ������ǰʱ����Ϊ1��wal segment��СΪ64M��

����64M��С��־�ļ�����ʽ���ɼ����lsn��segment��Ÿ�32λΪ0x0��segment��ŵ�λΪ0x7�� �������Ϊ0x90��xlog�ļ���Ϊ000000010000000000000007
ʹ��pg_xlogfile_name_offset()���Բ�ѯlsn��Ӧ���ļ����ļ���ƫ�ƣ�����������һ�¡�

![pg_current_xlog_location](media/2017-10-22-How-to-use-PostgreSQL-backup-and-restore-well-3.png)

### 2.checkpoint��control�ļ�
PostgreSQL�������ļ�����־�ļ���Ϊ���ࡣ��ĳlsn֮ǰ�Ĳ����Ѿ�ȫ��д���������ļ������lsn��֮ǰ����־�ļ����Զ�����checkpoint����ʵ�ִ˹��ܡ�

checkpoint���������³���ִ�У�����Ա�ֹ�ִ��check������ݿ�������ɻָ������ݿ������رգ��Լ���̨Checkpoint���̵Ķ���ִ�С�

checkpoint���̿��Լ�����Ϊ�����ȹ���checkpoint��¼��redo�ֶ�Ϊ��ǰ��д����־�ļ���lsn����Ȼ�����ݻ������е�������д����̣����д��checkepoint��־��¼������checkpoint��¼��������checkpoint��¼д��control�ļ���

512�ֽڵ�control�ļ���PostgreSQL�Ĺؼ����ݣ��������ݿ�����ʱ���ж����ݿ�״̬�ͻָ�λ�á�controlfile�ļ��м�¼�����ݿ��״̬�����checkpoint��¼����С�ָ�lsn��Ϣ�ͻ����Ĳ������á����ݿ��״̬������
* DB_SHUTDOWNED�����ݿ������رգ�
* DB_SHUTDOWNED_IN_RECOVERY�����ݿ��ڻָ�ʱ�رգ�
* DB_SHUTDOWNING�����ݿ������������رչ����б�����
* DB_IN_CRASH_RECOVERY�����ݿ��ڻָ������б�������
* DB_IN_ARCHIVE_RECOVERY�����ݿ⴦�ڹ鵵�ָ���
* DB_IN_PRODUCTION�����ݿ⴦����������״̬���ȴ�����������

### 3.��־�ļ���������鵵
PostgreSQL��־�ļ���segment��Ŵ�1��ʼ��һ����־�ļ�д��󣬻�д����һ����ŵ���־�ļ���checkpoint֮�����һ��checkpoint.redo lsn֮ǰ����־�ļ����Զ�����PostgreSQL��ѭ��ʹ����־�ļ���checkpoint�����У��Ὣ�ɶ�������־�ļ�����Ϊδ������־�ļ�����������־�ļ����³�ʼ����PostgreSQL��д�µ���־�ļ�ʱ��������ļ��Ѵ��ڣ���ʹ�ø��ļ�������Żᴴ���µ��ļ�����˲��ܴ�pg_xlogĿ¼�е��ļ���ֱ���жϵ�ǰ����־�ļ�����Ҫʹ��pg_current_xlog_location��pg_xlogfile_name_offset���������жϡ�

Ϊ�־ñ�����־�ļ�����Ҫ������־�鵵ģʽ���ڸ�ģʽ�£��ɶ�����־�ļ���ɾ��ǰ����������ָ��Ŀ¼����postgres.conf�����ļ�����������������

    wal_level=replica �����
    archive_mode = on
    archive_command = 'cp %p /mnt/server/archivedir/%f'
    %p��ʾpg_xlogĿ¼·������־�ļ�����%f��ʾ��־�ļ����� ��־��������/mnt/server/archivedirĿ¼

��־�Ĺ鵵�������£�
* checkpoint�����У���һ����־�ļ�X�ɶ���ʱ����pg_xlog��archive_statusĿ������X.ready�ļ���
* ��̨archive���̸�����־�ļ��Ŀ������ý��̼��archive_statusĿ¼����������X.ready�ļ�����ʹ��archive_command�����ļ�������X.ready����ΪX.done
* ��һ��checkpoint�����У���archive_statusĿ��X.done��Ӧ��X��־�ļ�������

### 4.crash recovery
PostgreSQL���������У�ֱ��kill�����̣�����PostgreSQL��������crash recovery�������̣���control�ļ���checkpoint��redo lsnλ�ÿ�ʼ��
ʹ��pg_xlogĿ¼�е���־�ļ����лָ���PostgreSQL�ܽ���������������Ϊ����״̬�������checkpoint��¼����control�ļ��С�

��ʼ�����ݿ��control�ļ�DB״̬��ʼֵΪshutdown��pg����ʱ����control�ļ�DB״̬Ϊshutdown����״̬����Ϊproduction���˳��ָ����̡��������رշ���ʱ��ִ��checkpoint������control�ļ�DB״̬����shutdown��pg����ʱ����control�ļ�DB״̬Ϊproduction����˵��������crash�����control�ļ���ȡ���checkpoint����redo lsn��ʼ���лָ����ָ���ɺ󣬽�״̬����Ϊproduction��


### 5.�ȱ�
���ݷ�Ϊ�䱸���ȱ����䱸�������رշ���󿽱��ļ����ȱ��Ƿ������������п����ļ������ڲ������ݻ��������ƣ��������ļ����ݻ᲻һ�¡��������ݿ�ָ�����ԭ��ֻҪȷ��ĳlsn֮ǰ����־�Ѿ�ȫ��д���������ļ������ڿ�����������ļ��ϣ�Ӧ�ø�lsn��֮�����־�ļ����ɽ����ݻָ���һ�µ�״̬��

�ȱ��������²���
* ִ��pg_start_backup����:�ú���ִ��checkpoint����checkpont��Ϣд������Ŀ¼�µ�backup_label�ļ���
* ��������Ŀ¼��ָ��λ��
* ִ��pg_stop_backup����:������ɾ��backup_label�ļ���дXLOG_BACKUP_END��־������pg_xlogĿ¼��д��backup�ļ������ļ���¼���ȱ���ʼ�ͽ�����lsn��Ϣ��

backup�ļ���ʽΪ���ȱ���ʼlsn��Ӧ����־�ļ���.��ʼlsn�Ŀ���ƫ��.backup

### 6.ʹ�ù鵵��־�ָ�

Crash recoveryֻ��ʹ��pg_logĿ¼�е���־�ļ����лָ�������archive recoveryģʽ�󣬿���ʹ������Ŀ¼����־�ļ����鵵��־�ļ������лָ���

������Ŀ¼�洴��recover.conf�ļ���PostgreSQL����ʱ����ȡ�����ļ��������archive recovery���̡���recover.conf��������־��������restore_command��pg�ָ������У�ʹ�ø�����鵵��־������pg_xlogĿ¼����лָ���

    restore_command = 'cp /mnt/server/archivedir/%f "%p"'
    %f��ʾ��־�ļ��� %p��ʾĿ��·�����ļ���

### 7.ʹ�������ƻָ�
�����ƿ�����Ϊarchive recovery��һ�������ʹ�ù鵵��־�ļ����лָ�ʱ��������Ҫ��ȡ����һ������xlog�ļ����ſɽ��лָ������������У�����������־��¼�󣬻ἰʱ���͵�������

��slave�ڵ�����Ŀ¼��recover.conf�У����õ�������������Ϣprimary_conninfo������standby_modeΪon��
    
    standby_mode = 'on'
    primary_conninfo = 'host=192.168.1.50 port=5432 user=foo password=foopass'

master�ڵ��postgres.conf�ļ���ָ��wal_level�ͷ�����־���̵���Ŀmax_wal_senders��
    
    wal_level=replica �����
    max_wal_senders=5

��master��pg_hba.conf�ļ������������ӽ���
    
    host    replication     postgres        192.168.10.0/24            trust

slave�����������wal reciver���̣�����primary_conninfo��master������������master�յ����������wal sender���̣�wal sender��reciver�������ӡ� wal reciver����ʼ��lsn��Ϣ���͸�wal sender��wal sender�Ӹ�lsn��ʼ������־��¼�������͸�wal reciver��wal reciver����־д��pg_xlogĿ¼�е���־�ļ�����֪ͨ�ָ����̶�ȡ�ļ����лָ�����

### 8.�ָ����˳���ʱ����

Crash recoveryģʽ�£�Ӧ����pg_xlogĿ¼�е����п�����־�ļ����Զ��˳��ָ�����������״̬��Archive recoveryģʽ�£�recovery.conf�ļ��в���standby_modeΪoffʱ��Ӧ����������־���Զ��˳��ָ�����������״̬��standby_modeΪonʱ��Ӧ����������־�󣬻ָ����̲����˳���������ȡ������־�������ڹ鵵��־�ļ��������ƣ������յ�pg_ctl���߷�����promote����󣬲��˳��ָ����̣���������״̬��

����ͨ������Recovery Target��ʹ��archive recovery��ָ����λ�ã�ʱ�������ţ�ֹͣ�ָ�����recovery.conf�ļ��������²�������ʾ�ָ������ڻָ���123947����������

    recovery_target_xid = '123947'

ʱ���ߣ�Timeline����PostgreSQL�е����еĸ�����ʼֵΪ1���˳�archive recoveryʱ��timeline��1���˳�crash recoveryʱ��timeline���䡣Timeline��ӳ����־���ļ����У���־�ļ���������ʽΪ��ʱ���ߺ�+segment��Ÿ�λ+segment��ŵ�λ��

����ʱ���߸������־λ�õ�Ψһ��ʶ��lsn��Ϊʱ����+lsn��checkpoint�Ľṹ�м�¼�˵�ǰ��timeline��

����ʱ�����л�ʱ����pg_xlogĿ¼д��ʱ����history�ļ����ļ���Ϊ"��ǰtimelime.history"���ļ��ڼ�¼��ʱ�����л�����ʷ��¼��ÿһ�м�¼һ��ʱ������Ϣ����ʽΪ<parentTLI> <switchpoint> <reason>��


parentTLIΪʱ����id��<switchpoint>Ϊ�л��������lsn��<reason>Ϊ�����л���ԭ��

��ʱ����history�ļ��У����Լ����ÿ��ʱ���ߵĿ�ʼ�ͽ���lsn��

    ʱ�����ļ�00000003.history������Ϊ 
    1	0/14000060	no recovery target specified
    2	0/140420D0	no recovery target specified

���ļ�����Ϊ��ǰʱ����Ϊ3��ʱ����1��lsn��Χ[0/0,0/14000060)��
ʱ����2��lsn��Χ[0/14000060,0/140420D0)��ʱ����3��0/140420D0��ʼ��


ʹ��timeline�������ŵ㣺
* �л��߼��Ե���������ʱ����history�ļ������Լ����ÿ��ʱ���ߵĿ�ʼ�ͽ���lsn��
* ����鵵��־�ĸ��ǡ��������������Ĺ鵵Ŀ¼��ͬʱ����������Ϊ���������ɵ���־�ļ�����ԭ������ͬ��ʱ���߲�ͬ�����������鵵Ŀ¼�󣬲��Ḳ��֮ǰ����־�ļ���


### 9��pg_basebackup��pg_rman����
pg_basebackup��pg_rmanΪ������ָ��ṩ���õĲ���������棬�����ֹ����������ļ���

pg_basebackup��PostgreSQL�Դ���һ��Զ���ȱ����ߣ����Խ�Զ��PostgreSQL�ȱ�������Ŀ¼���乤������Ϊ�����ӵ�һ��Զ��PostgreSQL��ִ��pg_start_backup������������Ŀ¼���䵽���أ�ִ��pg_stop_backup���

    ����ַΪ192.168.0.1��PostgreSQL�����ݵ�����usr/local/pgsql/dataĿ¼
    pg_basebackup -h 192.168.0.1 -U test -D /usr/local/pgsql/data

pg_basebackup֧����Ŀ������Ŀ¼�������������Ƶ�recovery.conf�ļ���

    pg_basebackup -h 192.168.0.1 -U test -R -D /usr/local/pgsql/data

����/usr/local/pgsql/dataĿ¼�������������õ�postgresql.conf�ļ�����������

    standby_mode = 'on'
    primary_conninfo = 'host=192.168.0.1 user=test'

pg_rman��PostgreSQL�ı�����ָ����ߣ�֧��ȫ�����������鵵���ֱ���ʽ��֧������ѹ���뱸�ݼ�����pg_rman�����ڴ����������ݿ���������ݡ�pg_rman�����뱻�������ݿⰲװ��ͬһ̨�������䱸������Ϊ�����ӵ�����PostgreSQL��ִ��pg_start_backup��ȫ�������ļ�����ͨ���Ƚ������ļ����lsn�Ž����������ݣ�ִ��pg_stop_backup������ݹ鵵��־��

pg_rman �ָ�֧�ֽ����ݻָ���ָ��ʱ�䡢����ź�ʱ���߲���������Ϊ�佫��Ӧ��ȫ�����ݺ͹鵵��־��������ӦĿ¼��������recovery.conf�ļ���restore_command������standby_modeΪoff��
pg_rman֧�ֵ��������
* ��ʼ�� pg_rman init
* ȫ������ pg_rman backup -b full
* �������� pg_rman backup -b incremental  
* �ָ� pg_rman restore

# ����PostgreSQL���ݿ�ָ�����
���������ļ��Ͳ����Ĳ�ͬ��PostgreSQL�ָ����������·��ࡣ 

![�ָ�����](media/2017-10-22-How-to-use-PostgreSQL-backup-and-restore-well-4.png)

Crash recovery��PostgreSQL�������Ϻ��Զ����еĻָ�����archive recovery��DBAͨ������recovery.conf�ļ���PostgreSQL���������Ļָ����̡�

����recovery.conf�ļ���standby_mode����Ϊon��off�����Կ��ƽ���standbģʽ���Ƿ�standbyģʽ����standbyģʽ�£�PostgreSQL�ָ���ָ��λ�û��߷���û�п�����־��¼ʱ��ֹͣ�ָ����̡�standbyģʽ�£���û�п�����־������£��������鲢Ӧ�ÿ�����־��ֱ��DBA����promote���

����postgresql.conf�ļ���hot_standby����Ϊon��off�����Կ����Ƿ���hot standbyģʽ��hot standby��������£��ָ�����ǰ�����ݿ�ɶ����ṩֻ�����ʡ�hot standby�ر�����£��ָ�����ǰ�����ݿⲻ�ṩ������ʡ�

5������������ļ�������Ĳ�ͬ��
* crash recovery����recovery.conf�ļ�
* archive recovery����recovery.conf�ļ���lable�ļ�����ѡ��
    * standby-hot standby��standby_modeΪon��hot_standbyΪon
    * standby-��hot standby��standby_modeΪon��hot_standbyΪoff
    * ��standby-hot standby��standby_modeΪoff��hot_standbyΪon
    * ��standby-��hot standby��standby_modeΪoff��hot_standbyΪoff

���������ƽ������archive recovery-standby-hot standby���ã����ڻ�������+�鵵��־�ָ������ã��������archive recovery-��standby-hot standby���á�

Recovery���̼�˵���Ǵ�һ��checkpoint��redo lsnλ�ÿ�ʼ��ͨ��Ӧ����־��¼��ʹ�����ļ��ﵽһ�µ�״̬������ÿһ�ָֻ����ã�Ҫ��ȷ�������⣬�������ҵ���ʼ��lsn��ʱ���ߣ���־��¼����Դ������ָ�״̬����˳���

Crash recoveryģʽ�£���control�ļ���ȡcheckpoint��¼�����а���redo lsn��ʱ���ߣ��Ӹ�λ�ÿ�ʼ�ָ�����־��¼ֻ����pg_xlogĿ¼�е���־�ļ�����û����־����Ӧ��ʱ���˳��ָ���

Archive recoveryģʽ�£�������Ŀ¼�²�����backup_label�ļ�ʱ����crash recovery��ͬ�ķ�ʽ��control�ļ���ȡredo lsn��ʱ���ߡ�������Ŀ¼�´���backup_label�ļ�ʱ��redo lsn�Ӹ��ļ���ȡ������timeline history�ļ�����ȡ��redo lsn��Ӧ��ʱ���ߡ�

Archive recoveryģʽ�ķ�standby�����£���������recovery.conf��restore_command�����ģʽ��ֻ��ʹ�ù鵵��־�ļ����лָ���Ӧ�������еĹ涨��־������ָ��λ��ʱ���ָ����������

Archive recoveryģʽ��standby�����£���������recovery.conf��restore_command�����primary_conninfo�е�һ������ģʽ�¿���ʹ�ù鵵��־�ļ����������ơ���û�п��õ���־��¼ʱ���������鲢Ӧ�ÿ�����־��ֱ��DBA����promote���

��recovery.conf�ļ��У���������Recovery Target��ʹ��archive recovery��ָ����λ�ã�ʱ�䡢����Ż�ʱ���ߣ�ֹͣ�ָ���

## �ġ�PostgreSQL�߿��÷����еı�����ָ�

PostgreSQL�߿��÷���Ӧ�ܹ�������ʹ��ϻָ���ʵʱ�����л�����������ݻָ��Ͳ鿴��ʷ���ݵ�����

�߿��û����Ľ������������¹�����

### ��������������־�鵵�����������ڵ���Ϣ

postgres.conf���첽�����ƣ�

    wal_level=replica

    archive_mode = on

    archive_command = 'cp %p /mnt/server/archivedir/%f'

    max_wal_senders=5 #����wal��������

    hot_standby=on

pg_hba.conf

    host    replication     postgres        192.168.10.0/24            trust

### ��������������������

ʹ��basebackup�����ȱ���

    pg_basebackup -h 192.168.0.1 -U test -R -D /usr/local/pgsql/data

�޸�postgres.conf�е�port��archive_commandΪ�����˿ں͹鵵·�����������������������ơ�

���������£������ָ�ģʽΪarchive recovery������standby������hot standby��

### ʹ��pg_rman����Ϊ���������������ݱ��ݣ������ڽ����������ݱ���

* ��ʼ�� pg_rman init -B �����ļ�����Ŀ¼ -D ���ݿ�����Ŀ¼

* ȫ������ pg_rman backup -B �����ļ�����Ŀ¼ -D ���ݿ�����Ŀ¼ -b full

* �������� pg_rman backup -B �����ļ�����Ŀ¼ -D ���ݿ�����Ŀ¼ -b incremental  


### ���ϴ������̣�

��1���ڻ���������״̬��ع��ߣ�ʵʱ�������״̬������������ʱ���Զ�promte�������������ݿ����·�ɵ�������

��2���ָ���ʷ����

pg_rman restore����֧�ֽ����ݻָ���ָ��ʱ�䡢����ź�ʱ���߲������������Ӧ��ȫ�����ݺ͹鵵��־��������ӦĿ¼��������recovery.conf�ļ���
pg_rman restoreִ����ɺ�����PostgresSQL�����лָ���

���������£������ָ�ģʽΪarchive recovery���ر�standby������hot standby��

### �塢��β

ͨ������PostgreSQL���ݿⱸ����ָ����̵�����ļ���������������Ҫ���̣��Իָ���ʽ�����˷��࣬�����߿��÷����б�����ָ��Ļ������á������Ŀ����Է����У�����Ҫ��������״̬��أ����ݷ���·���л��͹����������õ����⡣

----

��Ȩ����������ת��-������-������-��������[�����⹲��3.0���֤��](https://creativecommons.org/licenses/by-nc-nd/3.0/deed.zh)