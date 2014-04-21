all:
	@echo -ne "generate R.java..."
	@apkutil genrjava ./gen
	@echo "Done"
	@#@echo "genereate source via aidl"
	@#@apkutil aidl -I./src -o./gen src/com/cjacker/hello/*.aidl
	@#@echo "Done"
	@echo -ne "compile source codes..."
	@apkutil javac src/com/cjacker/hello/*.java gen/com/cjacker/hello/*.java -d bin
	@echo "Done"
	
	@rm -rf build
	@mkdir -p build
	
	@echo -ne "generate dex file..."
	@apkutil dx --dex --output=./build/classes.dex ./bin
	@echo "Done"
	
	@echo -ne "prepare project directory..."
	@cp -r res build 
	@cp -r *.xml build
	@cp -r *.yml build
	@echo "Done"
	
	@echo "generate HelloWorld.apk..."
	@apkutil enapk build HelloWorld.apk
	
	@echo -ne "sign HelloWorld.apk..."
	@apkutil sign HelloWorld.apk HelloWorld-signed.apk
	@echo "Done"
install:
	@echo -ne "Install apk to device..."
	@apkutil adb install HelloWorld-signed.apk
	@echo "Done"

clean:
	@rm -rf bin/*
	@rm -rf gen/*
	@rm -rf build 
	@rm -rf *.apk
