<h2>App Transport Securit</h2>

     <key>NSAppTransportSecurity</key>

        <dict>

           <key>NSAllowsArbitraryLoads</key>

           <true/>

        </dict>

<h2>NSUserDefault</h2>

      NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                     
      [defaults setObject:[@"Jabir" forKey:@"strVanue"];
                     
      [defaults synchronize];
                      
      NSLog(@"strVanue : %@",[defaults valueForKey:@"strVanue"]);
