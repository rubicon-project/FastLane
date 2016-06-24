# FastLane Integration Guide

##Overview


FastLane is called via a simple Javascript file included in the `<HEAD>` tag on the page to execute Rubicon Project Marketplace Auctions asynchronously prior to calling the primary Ad Server. The Ad Server can then be accurately informed of available demand from the Marketplace and therefore make better yield optimization decisions about which line item to render for any/all ad slots on any given page.
##Code Samples
- [Standard FastLane integration with DFP](IntegrationExamples/standard_gpt.html)
- [Slot Level - Adding first party data and setting slot position](IntegrationExamples/first_party_data_slot_gpt.html#L28)

- [Page Level - Adding first party data and contexts](IntegrationExamples/first_party_data_page_gpt.html#L30-L39)

- [Running individual slots - For infinite scroll/dynamic pages](IntegrationExamples/infinite_scroll_page_gpt.html#L30-L39)

- [Get ad server targeting (for non DFP ad servers)](IntegrationExamples/non_gpt_integration.html#L25-L59)

- [Render creative code (code to be trafficked inside ad server)](IntegrationExamples/creative_render.html)


##Custom Use Cases
<table style="width: 100%;">
  
  <tbody>
    
    <tr>
      
      <td>
        
        <div>
          
          <div>
            
            <p>
               Use Case 
            </p>
             
          </div>
           
        </div>
         
      </td>
      
      <td>
        
        <div>
          
          <div>
            
            <p>
               Proposed Solution 
            </p>
             
          </div>
           
        </div>
         
      </td>
       
    </tr>
    
    <tr>
      
      <td>
        
        <div>
          
          <div>
            
            <p>
               All ad units fall under 1 site and 1 zone, with varying sizes 
            </p>
             
          </div>
           
        </div>
         
      </td>
      
      <td>
        
        <div>
          
          <div>
            
            <ul>
              
              <li>
                 Only 1 ad slot mapping needed in the Rubicon backend config 
              </li>
              
              <li>
                 It should be set up as "catchAll" 
              </li>
               
            </ul>
             
          </div>
           
        </div>
         
      </td>
       
    </tr>
    
    <tr>
      
      <td>
        
        <div>
          
          <div>
            
            <p>
               Needs to differentiate desktop vs. mobile 
            </p>
             
          </div>
           
        </div>
         
      </td>
      
      <td>
        
        <div>
          
          <div>
            
            <ul>
              
              <li>
                 Set page context to "mobile" via rubicontag.addContext()o n the web page 
              </li>
              
              <li>
                Set up mobile specific slots in the backend config 
              </li>
               
            </ul>
             
          </div>
           
        </div>
         
      </td>
       
    </tr>
    
    <tr>
      
      <td>
        
        <div>
          
          <div>
            
            <p>
               Needs a way to match URLs/domains 
            </p>
             
          </div>
           
        </div>
         
      </td>
      
      <td>
        
        <div>
          
          <div>
            
            <ul>
               <li>Utilize urlPattern set up in the backend config</li>
            </ul>
             
          </div>
           
        </div>
         
      </td>
       
    </tr>
    
    <tr>
      
      <td>
        
        <div>
          
          <div>
            
            <p>
               Custom rules to map ad slot names 
            </p>
             
          </div>
           
        </div>
         
      </td>
      
      <td>
        
        <div>
          
          <div>
            
            <ul>
               <li>Create RegEx rules for the ad slot mapping creation</li>
            </ul>
             
          </div>
           
        </div>
         
      </td>
       
    </tr>
     
  </tbody>
   
</table>

##Custom Web Page Setup

<div title="Page 12">
  <table style="width: 100%;">
    <tbody>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Use Case
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <p>
                Proposed Solution
              </p>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Infinite Scroll/Dynamic Page Slot Definition
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <ul>
                <li>
                  Particular ad slots can be specified to be included for a Rubicon auction
                </li>
                <li>
                  Subsequent rubicontag.run() can be executed as the additional page slots are loaded
                </li>
              </ul>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Need a different way to retrieve key/value pairs, apart from setTargetingForGPTSlot()
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <ul>
              <li>
                getAdServerTargeting() can be used to get all or individual slots
      
              </li>
              <li>
                To get all of the targeting objects:&nbsp;
                
              </li>
              <li>
                To get targeting for an individual slot: window.rubicontag.getSlot('&lt;elementID&gt;').getAdServerTargeting();
              </li>
              <div title="Page 13">
                <p>
                  where elementID is the same that was passed to rubicontag.defineSlot
                </p>
              </div>
            </ul>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</div>

##Best Practices


<div title="Page 13">
  <table style="width: 100%;">
    <tbody>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Category
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <p>
                Recommendation
              </p>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Setting ATF/BTF
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <ul>
                <li> Always set the ATF or BTF in rubicontag.defineSlot().setPosition('atf')</li>
              </p>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Trafficking Creative Code
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <ul>
                <li>
                  &shy; &nbsp;Ensure that there are no character formatting issues with the creative code
                </li>
                <li>
                  &shy; &nbsp;Always use a text editor to edit the code prior to trafficking it into the Ad Server
                </li>
              </ul>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Bulk Assign Creative to Line Items
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <ul>
                <li>
                  &shy; &nbsp;Create the creative once per ad size
                </li>
                <li>
                  &shy; &nbsp;Once all the line items are done, assign the creative in bulk to all the line items of that size
                </li>
              </ul>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Troubleshooting
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <ul>
                <li>
                  Append '?rp_loglevel=4' or '#rp_loglevel=4' to the url to turn on logging
                </li>
                <li>
                  Overrides the log level for that site for the entire session until browser is closed (no need to append every time)
                </li>
              </ul>
            </div>
          </div>
        </td>
      </tr>
      <tr>
        <td>
          <div>
            <div>
              <p>
                Testing
              </p>
            </div>
          </div>
        </td>
        <td>
          <div>
            <div>
              <ul>
                <li>
                  Append '?rp_cpm_override=' or '#rp_cpm_override=' to the url to override the price of a request
                </li>
                <li>
                  Forces ads to render when they wouldn't otherwise
                </li>
              </ul>
            </div>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</div>