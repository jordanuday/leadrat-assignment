//     const seats = { "0": [0,0,0,1,2,3,4,0,5,], "1": [...] };
// Object.keys(seats).forEach(row => seatObject = seats[row].includes(seatNumber));



const [seats, setSeats] = useState(layout.map((item,index) => {
        const seatType = index > 1 ? "standard" : "premium"
        item.map((data) => (
            { id: data, isZero: !!data, isSelected: false, isBooked: false, type: seatType }))
    }))




const bookHandler = (seatId) => {
    
        if (ticketNumber === '') {
            toast.error("Please select ticket quantity")
        } else if (selectedSeats < ticketNumber) {
            let updatedSeat = seats.map(item => item.map(data => {
                if (data.id === seatId) {
                    if (data.isBooked) {
                        toast.error("This seat already Booked ... !")
                        return { ...data, isSelected: false }
                    } else {
                        if (data.isSelected) {
                            setSelectedSeats(selectedSeats - 1)
                            return { ...data, isSelected: false }

                        } else {
                            setSelectedSeats(selectedSeats + 1)
                            return { ...data, isSelected: true }
                        }
                    }

                } else {
                    return data
                }
            }))
            setSeats(updatedSeat)
        } else {
            toast.error("Quantity limit full ...!")
        }

    }
