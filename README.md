# Call-Several-actions-in-one-click

Example:

```
import React, { useState } from 'react';
import { View, TextInput, TouchableOpacity, Modal, StyleSheet, Text } from 'react-native';

// REDUX
import { connect } from 'react-redux';
import { addTodo } from '../../actions/todos';
import { toggleModal } from '../../actions/modal';

const AddTodoModal = ({ addTodo, modalVisibility, toggleModal }) => {
    const [todo, setTodo] = useState('');

    const handleChange = text => {
        setTodo(text)
    }

    const handleSubmit = () => {
        addTodo(todo)
        setTodo('')
        toggleModal()
    }

    return (
        <Modal visible={modalVisibility} animated='slide'>
            <View style={styles.screen}>
                <TextInput
                    placeholder='add new todo'
                    value={todo}
                    onChangeText={text => handleChange(text)}
                    style={styles.input}
                />
                <View style={styles.buttonView}>
                    <TouchableOpacity style={styles.button1} onPress={handleSubmit}>
                        <Text style={styles.text}>ADD</Text>
                    </TouchableOpacity>
                    <TouchableOpacity style={styles.button2} onPress={toggleModal}>
                        <Text style={styles.text}>CANCEL</Text>
                    </TouchableOpacity>
                </View>
            </View>
        </Modal>
    )
}

const styles = StyleSheet.create({
    screen: {
        display: 'flex',
        justifyContent: 'space-evenly',
        alignItems: 'center',
        flex: 1
    },

    buttonView: {
        display: 'flex',
        flexDirection: 'row',
        justifyContent: 'space-around',
        display: 'flex',
        flexDirection: 'row',
        justifyContent: 'space-between',
        width: '65%'
    },

    input: {
        width: 300,
        borderColor: 'black',
        borderWidth: 1,
        borderRadius: 5,
        fontSize: 20
    },

    button1: {
        backgroundColor: '#0373fc',
        padding: 20,
        width: 100,
        textAlign: 'center',
        display: 'flex',
        justifyContent: 'center',
        alignItems: 'center',
        borderRadius: 10
    },

    button2: {
        backgroundColor: '#ff2929',
        padding: 20,
        width: 100,
        borderRadius: 10
    },

    text: {
        color: 'white',
        fontSize: 15
    }
})

const mapStateToProps = state => {
    return {
        modalVisibility: state.modal
    }
}

export default connect(mapStateToProps, { addTodo, toggleModal })(AddTodoModal);
```
