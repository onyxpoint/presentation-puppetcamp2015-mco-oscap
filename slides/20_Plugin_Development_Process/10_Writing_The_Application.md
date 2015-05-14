## Writing the Application

* The User Interface to the System
* Independent Validation
* Receive and Process Results

```ruby
def main
  rpcutil = rpcclient('oscap') # The name of your agent goes here
  printrpc rpcutil.send(configuration[:command],configuration)
  
  printrpcstats :summarize => true
end
```
