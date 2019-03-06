# EOS multi_index
增: .emplace
删: .erase
改: .modify
查: .find    .get


做 .empalce 前先 .find 保证没有该数据

二级索引




code
scope 一般设置为 uint64_t 类型，表示调用的表所属（作用域）

# singleton

只有一条记录使用 singleton

singleton实际上是对multi_index类的一个简单封装。它将表名本身作为主键存储了一条记录，背后用的实际上还是multi_index。详情可以查阅EOS合约库源码：




# EOS inline


# EOS 相关网址
https://blockflow.net/t/topic/891
【EOS开发学习笔记】EOS.IO中的常见术语解释 https://www.jianshu.com/p/008bbf1f065b

智能合约之 eosio.cdt 我们需要知道的那些事 http://knowledge.cryptokylin.io/topics/99



nodeos -e -p eosio --plugin eosio::wallet_api_plugin --plugin eosio::chain_api_plugin --plugin eosio::account_history_api_plugin


## 错误
### 问题
```
Throw location unknown (consider using BOOST_THROW_EXCEPTION)
Dynamic exception type: boost::exception_detail::clone_impl<boost::exception_detail::error_info_injector<boost::program_options::unknown_option> >
std::exception::what: unrecognised option 'max-implicit-request'
```
### 修改方法
移除 
```
max-implicit-request
wallet-dir
unlock-timeout
```

### 问题
```
Not producing block because I don't have the private key for EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
```
### 解决方法
删除
```shell
signature-provider = FO6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV=KEY:5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

## 达成效果
全默认启动 EOS 私链


```
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/abi_bin_to_json
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/abi_json_to_bin
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_abi
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_account
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_block
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_block_header_state
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_code
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_code_hash
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_currency_balance
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_currency_stats
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_info
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_producer_schedule
info  2019-03-06T07:08:42.620 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_producers
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_raw_abi
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_raw_code_and_abi
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_required_keys
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_scheduled_transactions
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_table_by_scope
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_table_rows
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/get_transaction_id
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/push_block
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/push_transaction
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/chain/push_transactions
info  2019-03-06T07:08:42.621 thread-0  history_api_plugin.cpp:38     plugin_startup       ] starting history_api_plugin
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/history/get_actions
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/history/get_controlled_accounts
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/history/get_key_accounts
info  2019-03-06T07:08:42.621 thread-0  http_plugin.cpp:556           add_handler          ] add api url: /v1/history/get_transaction
```