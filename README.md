<h2>App Transport Securit</h2>

```javascript

     <key>NSAppTransportSecurity</key>
        <dict>
           <key>NSAllowsArbitraryLoads</key>
           <true/>
        </dict>

<h2>NSUserDefault</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController
     
     - (void)viewDidLoad
     {
          [super viewDidLoad];
    
          NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
          [defaults setObject:@"Jabir" forKey:@"strVanue"];
          [defaults synchronize];
     }


<h2>AlertView</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController
     
     - (void)viewDidLoad 
     {     
          UIAlertView *alert =  [[UIAlertView alloc]initWithTitle:@"Title" message:@"Message" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil];
          alert.tag = 101;
          [alert show];
     }
     
     - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex
     {
          if (alertView.tag == 101)
          {
               if (buttonIndex == 0)
               {
                    txtConfirmPass.text = @"";
                    txtNewPass.text = @"";
                    txtCurrentPass.text = @"";
               }
          }
     }
     
<h2>TextField Validation</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController
     
     - (IBAction)ActionButton:(id)sender
     {
          NSString *emailRegEx = @"[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}";
          NSPredicate *emailTest = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegEx];
          
          if(txtMobile.text.length == 0)
          {
               [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter Name" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
          }
          else if(txtMobile.text.length < 10)
          {
               [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter valid Phone Number" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
          }
          else if(txtMobile.text.length > 10)
          {
               [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter valid Phone Number" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
          }
          else if(txtEmail.text.length == 0)
          {
               [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter Email" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
          }
          else if([emailTest evaluateWithObject:txtEmail.text] == NO)
          {
               [[[UIAlertView alloc]initWithTitle:@"Alert" message:@"Please Enter valid Email" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil] show];
          }
      }
          
<h2>Push & Pop With StoryBoardID</h2>
     
     #import "ViewController.h"
     #import "SecondViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController

     - (IBAction)ActionPushButton:(id)sender
     {
          SecondViewController *push=[self.storyboard instantiateViewControllerWithIdentifier:@"SecondViewController"];
          [self.navigationController pushViewController:push animated:YES];
     }
     
     - (IBAction)ActionBackButton:(id)sender
     {
          [self.navigationController popViewControllerAnimated:YES];
     }

<h2>Push With Segue</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController

     - (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
     {
          if ([[segue identifier] isEqualToString:@"MySegue"])
          {
               // Get destination view
               SecondViewController *vc = [segue destinationViewController];
               vc.strPass = [NSString stringWithFormat:@"Jabir"];
          }
     }
     
     - (IBAction)ActionButton:(id)sender
     {
          [self performSegueWithIdentifier:@"MySegue" sender:sender];
     }
    
<h2>Push With Segue (tableView)</h2>

     #import "ViewController.h"
     @interface ViewController ()
     @end
     
     @implementation ViewController
     
     -(void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
     {
          if ([segue.identifier isEqualToString:@"pushSecond"]) 
          {
               NSIndexPath *indexpath=[tblView indexPathForSelectedRow];
               secondVc *ViewSecond=segue.destinationViewController;
               ViewSecond.strData=[NSString stringWithFormat:@"%@",[arr objectAtIndex:indexpath.row]];
          }
     }
     
     -(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
     {
          [self performSegueWithIdentifier:@"pushSecond" sender:nil];
     }
     
<h2>Pop & Back Button DataPass (StoryBoardID)</h2>

[Example](https://iostpoint.wordpress.com/2016/06/25/pass-data-back-to-previous-viewcontroller/)

ViewController.h

     #import <UIKit/UIKit.h>
     @interface ViewController : UIViewController
     
     @property (weak, nonatomic) IBOutlet UILabel *outputLabel;
     - (IBAction)ActionNext:(id)sender;
     
     @end
     
ViewController.m
     
     #import "ViewController.h"
     #import "SecondViewController.h"
     @interface ViewController ()
     
     @end

     @implementation ViewController
     
     - (IBAction)ActionNext:(id)sender
     {
          SecondViewController *acontollerobject=[self.storyboard instantiateViewControllerWithIdentifier:@"SecondViewController"];
          acontollerobject.delegate=self; // protocol listener
          [self.navigationController pushViewController:acontollerobject animated:YES];
     }
     
     -(void)sendDataToPreviousController: (NSString *)string
     {
          NSLog(@"Fired");
          self.outputLabel.text = string;
     }
     
SecondViewController.h
     
     #import <UIKit/UIKit.h>

     @protocol sendDataBack <NSObject>
     -(void)sendDataToPreviousController: (NSString *)string;
     
     @end

     @interface SecondViewController : UIViewController
     @property (assign,nonatomic) id delegate;
     
     @end
     
SecondViewController.m

     #import "SecondViewController.h"

     @interface SecondViewController ()<UITextFieldDelegate>
     @property (weak, nonatomic) IBOutlet UITextField *inputTextField;
     
     @end

     @implementation SecondViewController

     -(void)textFieldDidEndEditing:(UITextField *)textField
     {
          [_delegate sendDataToPreviousController:textField.text];
     }
     
