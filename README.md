# dotnet-cli

## Inputs
4 types of dotnet sub-commands are available
- restore
- build
- test
- publish

Based on each action type, different sets of inputs are needed. Please refer to list of available inputs

```YAML
- uses: snsinahub-org/dotnet-cli@main
  with:
    
    # full path of directory containing all dotnet projects
    # each dotnet project exist in a subdirectory in provided path
    # Action: build, restore, test, publish
    # example:
    #   path: 'C:\project'
    path: 'absolute-path-to-projects'    
    
    # directory path 
    # Action: test
    # example:
    #   test_path: 'C:\project\test'
    test_path: 'absolute-path-to-test-folder'
    
    # artifactory publish tag
    # Action: publish
    # example: 
    #   newTag: 'v1.0.0'
    newTag: ''
    
    # project configuration file extenstion 
    # Action: build, restore, test, publish
    # example:
    #   file_extenstion: '*.csproj'
    file_extenstion:
    
    # path to store artifact temporarily
    # Action: test, publish
    # example:
    #   temp_path: 'c:\tmp'
    temp_path:  
    
    # build type
    # Actions: build, test, publish
    # example:
    #   build_configuration: 'test'
    build_configuration:
    
    #  Number of levels to recurse 
    # Actions: test
    # example:
    #   test_depth: 2
    test_depth:
    
    # dotnet subcommand
    # Action: build, restore, test, publish
    # example:
    #   dotnet_action: build
    dotnet_action:
    
    
    # specifies if publish artifact is a web application or publish all projects
    # default true
    # action: publish
    # example:
    #   dotnet_web_publish: 'false'
    dotnet_web_publish:
    
```

## Build

```YAML
    - name: checkout
      uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '3.1.x' # SDK Version to use; x will use the latest version of the 3.1 channel
    - name: donet publish
      uses : snsinahub-org/dotnet-cli@main
      with:
        dotnet_action: 'build'
        path: 'C:\Users\Siavash Namvar\a'
        file_extenstion: "*.csproj"
        build_configuration: "release"
```

## Restore
```YAML
    - name: checkout
      uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '3.1.x' # SDK Version to use; x will use the latest version of the 3.1 channel
    - name: donet publish
      uses : snsinahub-org/dotnet-cli@main
      with:
        dotnet_action: 'restore'
        path: 'C:\Users\Siavash Namvar\a'
        file_extenstion: "*.csproj"
```

## Test
```YAML
    - name: checkout
      uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '3.1.x' # SDK Version to use; x will use the latest version of the 3.1 channel
    - name: donet publish
      uses : snsinahub-org/dotnet-cli@main
      with:
        dotnet_action: 'test'
        path: 'C:\Users\Siavash Namvar\a'
        temp_path: 'C:\Users\Siavash Namvar\a_temp'
        build_configuration: "release"                
        file_extenstion: "*.csproj"        
        test_path: "test_path"
        temp_path: "temp_path"
        test_depth:1        
```

## Publish

### Web application

```YAML
    - name: checkout
      uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '3.1.x' # SDK Version to use; x will use the latest version of the 3.1 channel
    - name: donet publish
      uses : snsinahub-org/dotnet-cli@main
      with:
        dotnet_action: 'publish'
        path: 'C:\Users\Siavash Namvar\a'
        temp_path: 'C:\Users\Siavash Namvar\a_temp'
        build_configuration: "release"
        newTag: "alpha.1.0.0"
        dotnet_web_publish: 'true'
        file_extenstion: "*.csproj"
```

## ALL

```YAML
    - name: checkout
      uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '3.1.x' # SDK Version to use; x will use the latest version of the 3.1 channel
    - name: donet publish
      uses : snsinahub-org/dotnet-cli@main
      with:
        dotnet_action: 'publish'
        path: 'C:\Users\Siavash Namvar\a'
        temp_path: 'C:\Users\Siavash Namvar\a_temp'
        build_configuration: "release"
        newTag: "alpha.1.0.0"
        dotnet_action: 'publish'
        dotnet_web_publish: 'false'
        file_extenstion: "*.csproj"
```