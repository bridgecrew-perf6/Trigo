test

## Trigo – DevOps Assignment

### General:

* Clone the following repo: https://github.com/trigodevops/test_repo.git  

* Work only on that repo (you got all the permissions that you need)  

* Create a new branch and work on it (not directly on master/main) 

* Please provide a descriptive readme file, so we know how to run your solution

* Solution needs to have the ability to scale

* The assignment is limited to 3 hours

### Stage 1:  
1. Deploy a multi env configuration solution anywhere you want with any tool that to want to use.

2. There are 2 (different) services and 3 Links:

    A. http(s)://`<ADDRESS>:<PORT>`/**prod**/service-a/config - will present production configuration of service a 

    B. http(s)://`<ADDRESS>:<PORT>`/**prod**/service-b/config - will present production configuration of service b

    C. http(s)://`<ADDRESS>:<PORT>`/**dev**/service-a/config  - will present dev configuration of service a

3. Each service will have its own config with accordance to the environment
4. Each service will respond with its config 
5. Don't copy the config to the app - inject it  
#### HINT:
Config should be hieratical, e.g:
```bash
├── base_config
│   ├── main_config
└── environments
    ├── dev
    │   ├── some_dev_config
    │   └── some_other_dev_config
    ├── production
        ├── some_prod_config
        ├── some_other_prod_config
```

### Stage 2:
1. Write/describe a process for rolling an update of a new app version, and deploying it to dev and then to prod
2. Write/describe a process for deployment of a configuration update (one of the values in the config file), which should trigger a restart of the app and result an update of the service response