## Writing the Agent: Functionality

1. Create your Scaffold
1. Add your *actions*
1. Rinse and Repeat

```ruby
module MCollective
  module Agent
    class Oscap<RPC::Agent
      require 'mcollective/agent/oscap/util'
      include MCollective::Agent::Oscap::Util

      require 'mcollective/agent/oscap/profiles'
      include MCollective::Agent::Oscap::Profiles

      action 'profiles' do
        get_profiles(xccdf(request))
      end
    end
  end
end
```
