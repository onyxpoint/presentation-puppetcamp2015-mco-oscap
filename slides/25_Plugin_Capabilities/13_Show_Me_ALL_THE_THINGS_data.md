## Yep, That's a LOT of Data

```shell
$ mco oscap scan -p rht-ccp -i ALL -f
```

```bash
master
   Scan Results: {"partition_for_tmp"=>{
                    :severity=>"low",
                    :result=>"fail"
                  },
# 71 More Results...
                  "sshd_use_approved_ciphers"=>{
                    :severity=>"medium",
                    :result=>"fail"
                  }}
          Score: 64.405869

Summary of Score:

   64.405869 = 1

Finished processing 1 / 1 hosts in 10236.46 ms
```
