## Writing the Agent: DDL

```ruby
action 'scan', :description => 'Run an OpenSCAP scan.' do
  display :always

  # Required Parameters
  input :profile,
    :prompt       => 'Profile Name',
    :description  => 'A specific Profile to run.',
    :type         => :string,
    :validation   => '.*',
    :optional     => false,
    :maxlength    => 1024

  output :score,
    :description  => 'OpenSCAP Scan Score',
    :display_as   => 'Score',
    :default      => '0'

  summarize do
    aggregate summary(:score)
  end
```

