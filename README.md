# -Travel-Itinerary-Planner-Agent
Travel Itinerary Planner Agent is an AI-based application that creates personalized travel plans based on the user's destination, budget, travel duration, interests, and transportation. It generates day-wise itineraries, estimates expenses, suggests local food, activities, and weather tips for a smooth trip.

# Install the latest Google GenAI library
!pip install -q -U google-genai


# Import required libraries
from google import genai
from IPython.display import display, Markdown


# Enter your Gemini API Key
API_KEY = "YOUR_GEMINI_API_KEY"

# Create Gemini client
client = genai.Client(api_key=API_KEY)



# Function to Generate Travel Itinerary
 
def generate_itinerary(destination,
                       budget,
                       duration,
                       interests,
                       transport):

    # Prompt sent to Gemini
    prompt = f"""
You are an AI Travel Planner.

Create a complete travel itinerary.

Destination:
{destination}

Budget:
{budget}

Travel Duration:
{duration}

Interests:
{interests}

Transportation:
{transport}

Requirements

1. Create a day-wise travel plan.
2. Recommend tourist attractions.
3. Suggest local food.
4. Include estimated expenses.
5. Mention transportation tips.
6. Return only the itinerary.
"""

    # Generate response using Gemini
    response = client.models.generate_content(
        model="models/gemini-3.5-flash",
        contents=prompt
    )

    return response.text



# Function to Modify Existing Itinerary

def modify_itinerary(plan, changes):

    prompt = f"""
Modify this travel itinerary.

Current Plan:

{plan}

Requested Changes:

{changes}

Return only updated itinerary.
"""

    response = client.models.generate_content(
        model="models/gemini-3.5-flash",
        contents=prompt
    )

    return response.text



# Function to Estimate Travel Expenses

def estimate_expenses(plan):

    prompt = f"""
Based on this itinerary

{plan}

Provide a detailed expense estimate.

Include

Accommodation

Food

Transportation

Entry Tickets

Shopping

Return only the expense summary.
"""

    response = client.models.generate_content(
        model="models/gemini-3.5-flash",
        contents=prompt
    )

    return response.text



# Function to Recommend Local Food & Activities

def food_activity(plan):

    prompt = f"""
Based on this itinerary

{plan}

Recommend

Local food

Popular activities

Shopping places

Nightlife (if applicable)

Return only recommendations.
"""

    response = client.models.generate_content(
        model="models/gemini-3.5-flash",
        contents=prompt
    )

    return response.text



# Function to Provide Weather Suggestions

def weather_tips(destination):

    prompt = f"""
Provide travel weather tips for

{destination}

Include

Best clothing

Best travel time

Safety precautions

Return only suggestions.
"""

    response = client.models.generate_content(
        model="models/gemini-3.5-flash",
        contents=prompt
    )

    return response.text


# Import Markdown display
from IPython.display import display, Markdown

# Store generated itinerary
plan = ""

# Store destination name
destination = ""



# Main Menu

while True:

    print("\n====================================")
    print("   TRAVEL ITINERARY PLANNER AGENT")
    print("====================================")
    print("1. Generate Itinerary")
    print("2. Modify Itinerary")
    print("3. Estimate Expenses")
    print("4. Local Food & Activities")
    print("5. Weather Suggestions")
    print("6. Exit")

    # Read user's choice
    choice = input("\nEnter Choice : ")

    # ---------------- Generate Itinerary ----------------
    if choice == "1":

        destination = input("Destination : ")
        budget = input("Budget : ")
        duration = input("Travel Duration : ")
        interests = input("Interests : ")
        transport = input("Transportation : ")

        print("\nGenerating your travel itinerary...\n")

        # Generate itinerary
        plan = generate_itinerary(
            destination,
            budget,
            duration,
            interests,
            transport
        )

        print("\n========== TRAVEL ITINERARY ==========\n")
        display(Markdown(plan))

        print("\n✅ Travel Itinerary Generated Successfully!")
        print("You can now choose Options 2–5.")

    # ---------------- Modify Itinerary ----------------
    elif choice == "2":

        if plan == "":
            print("\n⚠ Please generate an itinerary first.")
            continue

        changes = input("Enter Changes : ")

        plan = modify_itinerary(
            plan,
            changes
        )

        print("\n========== UPDATED ITINERARY ==========\n")
        display(Markdown(plan))

    # ---------------- Expense Estimation ----------------
    elif choice == "3":

        if plan == "":
            print("\n⚠ Please generate an itinerary first.")
            continue

        result = estimate_expenses(plan)

        print("\n========== EXPENSE ESTIMATION ==========\n")
        display(Markdown(result))

    # ---------------- Food & Activities ----------------
    elif choice == "4":

        if plan == "":
            print("\n⚠ Please generate an itinerary first.")
            continue

        result = food_activity(plan)

        print("\n========== LOCAL FOOD & ACTIVITIES ==========\n")
        display(Markdown(result))

    # ---------------- Weather Suggestions ----------------
    elif choice == "5":

        if destination == "":
            print("\n⚠ Please generate an itinerary first.")
            continue

        print("\nGenerating Weather Suggestions...\n")

        result = weather_tips(destination)

        print("\n========== WEATHER SUGGESTIONS ==========\n")
        display(Markdown(result))

    # ---------------- Exit Program ----------------
    elif choice == "6":

        print("\n🙏 Thank You For Using Travel Itinerary Planner!")
        break

    # ---------------- Invalid Choice ----------------
    else:

        print("\n❌ Invalid Choice. Please try again.")




#example output:
====================================
   TRAVEL ITINERARY PLANNER AGENT
====================================
1. Generate Itinerary
2. Modify Itinerary
3. Estimate Expenses
4. Local Food & Activities
5. Weather Suggestions
6. Exit

Enter Choice : 1
Destination : tirupathi
Budget : 1000
Travel Duration : 3
Interests : temples
Transportation : train

Generating your travel itinerary...


========== TRAVEL ITINERARY ==========

3-Day Tirupati Budget Temple Itinerary
Destination: Tirupati, Andhra Pradesh, India
Duration: 3 Days
Total Budget: ₹1,000 INR (Ultra-Budget/Pilgrim-style)
Theme: Temples & Pilgrimage
Primary Mode of Travel: Train (Arrival/Departure) & Public Buses
Day 1: Arrival & Tirupati Town Temples
Morning:
Arrive at Tirupati Main Railway Station (TPTY).
Walk to TTD Srinivasam Amenities Complex (located right opposite the RTC bus stand) or Vishnu Nivasam (opposite the Railway Station).
Check-in at the TTD Dormitory hall. Locker deposit: ₹100 (refundable), bed charges: ₹50/day.
Afternoon:
Board an APSRTC local bus from the bus stand to Tiruchanur (₹20).
Visit Sri Padmavathi Ammavari Temple (Goddess Laxmi). Opt for the Free Darshan line.
Lunch: Enjoy a budget South Indian meal/Thali at a local mess near the temple (₹80).
Evening:
Return to the town center by local bus (₹20).
Visit Sri Govindaraja Swamy Temple, located near the railway station (Free Entry). Walk around the ancient temple corridors.
Night:
Dinner: Local tiffin center (Idli/Dosa) near the station (₹50).
Overnight stay at TTD Dormitory (₹50).
Day 2: The Divine Ascent to Tirumala
Early Morning (4:00 AM):
Take a shared auto or local bus from Tirupati to Alipiri Toll Gate (₹20).
Begin the pedestrian climb via the Alipiri Footpath (3,550 steps, ~4 hours). It is a scenic, spiritual walk with drinking water and shelter facilities.
Mid-Day:
Reach Tirumala (the hill town).
Store your luggage and footwear at the free TTD security counters.
Join the Sarvadarsanam (Free Darshan) queue line for the main Sri Venkateswara Swamy Temple. (Wait times vary; plan for 3–6 hours).
Lunch:
Have a free, unlimited sacred lunch at the massive Matrusri Tarigonda Vengamamba Annaprasadam Complex in Tirumala (₹0).
Afternoon/Evening:
Have Darshan of Lord Venkateswara.
Collect one free Laddu prasadam associated with your free entry. Purchase an extra Laddu if desired (₹50).
Night:
Board a downhill APSRTC bus from Tirumala to Tirupati bus stand (Ghat road journey, ₹55).
Dinner: Light tiffin (Upma or Parotta) at Tirupati railway station circle (₹50).
Overnight stay at TTD Dormitory (₹50).
Day 3: Waterfalls, Caves & Departure
Morning:
Take a local bus/shared auto to Kapila Theertham (₹20).
Visit Sri Kapileswara Swamy Temple, the only Shiva temple in Tirupati, located at the foothills of Tirumala with a sacred waterfall flowing into the temple tank.
Mid-Day:
Walk or take a shared auto to the ISKCON Temple Tirupati (Lotus Temple) nearby (₹20). Enjoy the peaceful chanting halls and architecture.
Lunch:
Have a budget lunch at a local eatery near Kapilatheertham (₹70).
Afternoon:
Head back to the dormitory, collect your luggage, and check out (Collect your locker deposit refund of ₹100).
Walk to the local market near Govindaraja Temple to buy local wooden toys or cheap souvenirs (Optional).
Evening:
Reach Tirupati Railway Station to board your return train.
Estimated Expense Breakdown (Per Person)
Expense Category	Details	Cost (INR)
Accommodation	2 Nights in TTD Dormitories (Srinivasam/Vishnu Nivasam)	₹100
Food & Water	Local tiffins, budget meals + Free Annaprasadam	₹300
Local Transport	APSRTC buses & Shared autos	₹175
Darshan Tickets	Free Darshan (Sarvadarsanam)	₹0
Laddus / Prasad	Extra Laddu purchases	₹50
Emergency/Misc	Water bottles, public toilets, locker deposits	₹150
Total Estimated Cost		₹775
Transportation & Travel Tips
Local Buses (APSRTC): Frequent green buses connect Tirupati to Tirumala and other local temples. They are highly economical compared to private auto-rickshaws.
TTD Free Buses: Once inside Tirumala, use the free green shuttle buses ("Dharma Radhams") to move between the queue complex, cottages, and the main temple.
Footpath Luggage Service: If climbing by foot from Alipiri, TTD offers free luggage transportation from the start of the footpath directly to Tirumala.
Dress Code: Traditional wear is strictly enforced for entering temples. Men must wear Dhoti/Kurta-Pyjama; women must wear Saree/Salwar Kameez.
ID Proof: Always carry a valid Govt ID card (Aadhaar Card/Voter ID) as it is mandatory for security checks and free darshan queue entries.

✅ Travel Itinerary Generated Successfully!
You can now choose Options 2–5.

====================================
   TRAVEL ITINERARY PLANNER AGENT
====================================
1. Generate Itinerary
2. Modify Itinerary
3. Estimate Expenses
4. Local Food & Activities
5. Weather Suggestions
6. Exit

Enter Choice : 4

========== LOCAL FOOD & ACTIVITIES ==========

Local Food
Andhra Meals (Thali): Try authentic, unlimited Andhra meals served on banana leaves at budget-friendly messes like Sri Vasavi Mess or Hotel Sri Sobhanachala near the railway station.
Traditional Tiffins: Savor local breakfast items like Ghee Karam Dosa, Idli with ginger chutney, and Vada at Hotel Bhimas or Ramgopal Mess.
Filter Coffee: Sip hot, traditional South Indian filter coffee served in brass tumblers at any local eatery around the Govindaraja Temple.
Tirupati Laddu & Prasadam: Aside from the iconic Laddu, try the Pulihora (tamarind rice) and Chakkera Pongali (sweet rice) offered as prasadam at the temples.
Popular Activities
Silathoranam (Natural Arch): Visit this unique geological wonder and national monument located on Tirumala Hills, believed to be millions of years old.
Srivari Museum: Explore the museum in Tirumala which houses ancient scriptures, stone carvings, historical weapons, and traditional temple artifacts.
Srivari Mettu Path: If you prefer a shorter climb than Alipiri, try this alternative walking route (1,120 steps, ~1.5 to 2 hours) which is historically significant and fully shaded.
Srivari Padalu: Visit the highest point on Tirumala hills to see the footprints believed to be of Lord Venkateswara.
Shopping Places
Gandhi Road & Bazaar Street: Bustling budget markets perfect for buying brass lamps, copper idols, copper vessels, and religious photo frames.
Lepakshi Handicrafts Emporium: A government-run store near the town center ideal for buying authentic Andhra handicrafts, Kondapalli wooden toys, and Kalamkari textiles at fixed prices.
Tirumala Temple Outer Ring Shopping Complex: Shops offering wooden carvings, red sandalwood souvenirs (highly regulated, buy only from authorized sellers), and devotional music.
Nightlife (Pilgrim-style)
Tirumala Mada Streets Walk: Experience the peaceful, spiritual ambiance of walking around the brilliantly lit main temple complex at night.
Ghat Road Viewpoint: Stop at the designated viewpoints on the downhill Ghat road (while traveling by night bus) to see the breathtaking, glittering night view of Tirupati town.
Sahasra Deepalankarana Seva: Watch the evening procession of the Lord in Tirumala amidst thousands of lit lamps (visible from the outer corridors).

====================================
   TRAVEL ITINERARY PLANNER AGENT
====================================
1. Generate Itinerary
2. Modify Itinerary
3. Estimate Expenses
4. Local Food & Activities
5. Weather Suggestions
6. Exit

Enter Choice : 5

Generating Weather Suggestions...


========== WEATHER SUGGESTIONS ==========

Best Clothing
Temple Dress Code: Pack traditional Indian attire (Dhoti or Kurta-Pyjama for men; Saree, Half-Saree, or Salwar Kameez with Dupatta for women) as the Tirumala temple strictly enforces a traditional dress code.
Breathable Fabrics: Wear loose, light-colored cotton clothing to stay comfortable in the prevailing hot and humid weather.
Layering for Tirumala Hills: Bring a light sweater, cardigan, or shawl, as the hilltop area (Tirumala) can become quite chilly during early mornings, late evenings, and winter nights.
Footwear: Wear comfortable, easy-to-remove slip-on shoes or sandals, as footwear is not allowed inside temple premises.
Socks: Carry a pair of clean cotton socks to protect your feet from burning on the hot stone pathways during daytime temple visits.
Best Travel Time
Winter (November to February): This is the ideal time to visit, featuring pleasant weather with temperatures ranging from 15°C to 30°C, making sightseeing and queuing comfortable.
Avoid Summer (March to June): Temperatures can soar above 40°C, making the long wait times in queues and walking outdoors highly exhausting.
Monsoon Caution (July to October): Heavy rainfall can occur, which brings lush green landscapes but can also cause slippery conditions and travel delays on the ghat roads.
Safety Precautions
Hydration: Drink plenty of bottled water and carry electrolytes to prevent dehydration, especially while waiting in long queue lines.
Sun Protection: Apply high-SPF sunscreen, wear sunglasses, and carry an umbrella to protect against intense sun exposure.
Ghat Road Safety: Drive cautiously or hire experienced drivers for the winding uphill and downhill ghat roads connecting Tirupati and Tirumala, especially during rainy or foggy conditions.
Crowd and Security: Keep a close eye on your belongings, cash, and mobile phones in heavily crowded areas and temple queues to prevent pickpocketing.
Monkey Menace: Avoid carrying exposed food items, plastic bags, or flowers in open areas on Tirumala hills, as local wild monkeys can be aggressive in grabbing them.

====================================
   TRAVEL ITINERARY PLANNER AGENT
====================================
1. Generate Itinerary
2. Modify Itinerary
3. Estimate Expenses
4. Local Food & Activities
5. Weather Suggestions
6. Exit

Enter Choice : 6

🙏 Thank You For Using Travel Itinerary Planner!






        
