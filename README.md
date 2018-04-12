# Jlink-Sample
************ Greetings ***************  
javac -d mods/com.greetings src/com.greetings/module-info.java src/com.greetings/com/greetings/Main.java  
java --module-path mods -m com.greetings/com.greetings.Main  
************************** Greeting World *****************************  
javac -d mods/org.astro src/org.astro/module-info.java src/org.astro/org/astro/World.java  
javac --module-path mods -d mods/com.greetings src/com.greetings/module-info.java src/com.greetings/com/greetings/Main.java  
java --module-path mods -m com.greetings/com.greetings.Main  
************************* Packaging *************************  
jar --create --file=mlib/org.astro@1.0.jar --module-version=1.0 -C mods/org.astro .  
jar --create --file=mlib/com.greetings.jar --main-class=com.greetings.Main -C mods/com.greetings .  
******************** SERVICE ***************  
javac -d mods --module-source-path src $(find src -name "*.java")  
javac -d mods/com.greetings/ -p mods $(find src/com.greetings/ -name "*.java")  
java -p mods -m com.greetings/com.greetings.Main  
************************ JLINK *************************  
jlink --module-path $JAVA_HOME/jmods:mlib --add-modules com.greetings --output greetingsapp  
cd greetingsapp/bin  
./java -m com.greetings/com.greetings.Main  
