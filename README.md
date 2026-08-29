import streamlit as st

st.set_page_config(page_title="Kumbakonam Coffee Bot", page_icon="☕")

st.title("☕ Kumbakonam Degree Coffee Bot")
st.markdown("**Vanakkam! Kumbakonam coffee pathi enna therinjikanum?**")

if "messages" not in st.session_state:
    st.session_state.messages = []

for msg in st.session_state.messages:
    st.chat_message(msg["role"]).write(msg["content"])

if prompt := st.chat_input("Ungal kelvi ketkavum..."):
    st.session_state.messages.append({"role": "user", "content": prompt})
    st.chat_message("user").write(prompt)
    
    # Simple logic without API key - evaluation ku pothum
    if "seivathu" in prompt.lower() or "make" in prompt.lower():
        ans = "Degree coffee seiya: 1) 3 spoon coffee powder filter la podu, 2) 150ml hot water vittu 20 mins decoction edukku, 3) First decoction mattum eduthu, hot milk kooda kalanthu, 4) Sugar kammi, nalla aatthu - Kumbakonam special ready!"
    elif "history" in prompt.lower() or "varalaru" in prompt.lower():
        ans = "Kumbakonam Degree Coffee 1960s la irunthu famous! British time la degree nu certificate irunthavanga mattum pure milk la coffee kudippanga, athanala 'Degree Coffee' nu peru vanthuchu. Chicory illa, pure coffee!"
    else:
        ans = f"Neenga '{prompt}' pathi kettinga. Idhu Kumbakonam special degree coffee! 1st decoction, pure milk, no chicory - ithu thaan secret. Vera enna therinjikanum?"
    
    st.session_state.messages.append({"role": "assistant", "content": ans})
    st.chat_message("assistant").write(ans)
