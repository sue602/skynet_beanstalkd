# skynet_beanstalkd
beanstalkd for skynet(https://github.com/cloudwu/skynet.git)
modify from https://github.com/dualface/gbc-core.git


1. install beanstalkd from https://github.com/kr/beanstalkd.git
2. follow beanstalkd quick start :
	$ make
    $ ./beanstalkd

    
3. test

    local beanstalkd = require "beanstalkd"
	beanstalkd:connect()

	local ok, err = beanstalkd:use("mytube")
    if not ok then
        print("2: failed to use tube: ", err)
        -- return
    end

    local id, err = beanstalkd:put("myhello",2,2,2)
    print("beanstalkd put id=",id," error=",err)
    
    local ok, err = beanstalkd:watch("mytube")
    if not ok then
        print("watch error")
    end
    while true do
    	print("reserve==")
    	local result, err = beanstalkd:reserve(2)
    	dump(result,"result ====================== ")
    	if result ~=nil then
    		print("delet id=",result.id)
    		beanstalkd:delete(result.id)
    	else
    		break
    	end
    	-- print("skynet.sleep==")
    	-- skynet.sleep(100)
    end
   